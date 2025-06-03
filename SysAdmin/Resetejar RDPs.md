🔧 Steps from your local machine (with admin access to remote PC)
1. Open Command Prompt as Administrator
2. Find the RDP sessions on the remote PC:
```bash
query session /server:192.168.0.213
```
You should see output like this:
```graphql
 SESSIONNAME       USERNAME       ID   STATE     TYPE        DEVICE
 rdp-tcp#1         john.doe        2   Active    rdpwd
 console                           0   Conn      wdcon
```
Note the ID of the frozen session (e.g., 2).

Reset:

```sh
reset session 2 /server:192.168.0.213
```

Replace 2 with the actual session ID.