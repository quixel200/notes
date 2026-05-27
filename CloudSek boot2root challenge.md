We are provided with a URL to a web page. 
Looking at the source code, there is a file named `secrets.js` that has hardcoded credentials for a valid user, we can use this to login:

```
  const operatorLedger = [
    {
      codename: "relay-spider",
      username: "flightoperator",
      password: "GlowCloud!93",
      privilege: "operator",
    },
    {
      codename: "drift-marauder",
      username: "ghost",
      password: "aLongTimeAgo",
      privilege: "revoked",
    },
    {
      codename: "orbital-miner",
      username: "vector",
      password: "approximation",
      privilege: "revoked",
    },
  ];
```

looking at `login.js`, we can also see that the login token is set in sessionStorage and not in cookies

```
 sessionStorage.setItem("orbitalToken", response.token);
      sessionStorage.setItem("orbitalProfile", JSON.stringify(response.profile));
```

I tried tampering the JWT first by setting the algorithm to none and by removing the secret altogether, since that did not work I moved on with JWT cracking. 

I was able to crack the JWT and found that the secret is "butterfly"

![[Pasted image 20251214092318.png]]

We can now modify this JWT and get access to the admin beacon 

Looking at the logic of the admin beacon, we can submit a payload and it will first verify it with a checksum,

```
 if (adminForm) {
    adminForm.addEventListener("submit", async (event) => {
      event.preventDefault();
      const sessionToken = getSessionToken();
      if (!sessionToken) {
        adminResult.textContent = "Provide a valid token before transmitting.";
        return;
      }
      const message = adminMessage.value;
      const checksum = checksumInput ? checksumInput.value.trim() : "";
      const res = await fetch("/api/admin/hyperpulse", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${sessionToken}`,
        },
        body: JSON.stringify({ message, checksum }),
      });
      const data = await res.json().catch(() => ({}));
      if (!res.ok) {
        adminResult.textContent = data.error || "Beacon rejected the payload.";
        return;
      }
      adminResult.textContent = data.result;
    });
  }
```

The `verifyCheckSum` function is defined in the javascript file and we can use that to get valid checksums.

![[Pasted image 20251214100419.png]]

Since it says 'template' here, I tried SSTI and it worked as expected. 

![[Pasted image 20251214100448.png]]


Running the `id` command tells us that we are running as the root user.

![[Pasted image 20251214103217.png]]

We can now directly cat the root flag. 

![[Pasted image 20251214102004.png]]



