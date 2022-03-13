# Installing
It contains the steps that must be done during the installation of the module.
## Step One
We will make a few minor additions to the **acl.xml** file of the MTA server.

```xml
<acl name="Default">
   <right name="resource.MtaJS.http" access="false"></right>
</acl>
```
We will add a new right to the acl named Default.
This rule is important for **authorization**.
> If you don't add this Right anyone can use the system and get full access to your server!

## Step Two
```xml
<acl name="MtaJS">
   <right name="function.fetchRemote" access="true"></right>
   <right name="resource.MtaJS.http" access="true"></right>
</acl>
```
We will create a new acl and name it **MtaJS**. We add two rules in it.<br>
> These rules provide communication between the server and the client.

## Step Three
```xml
    <group name="MtaJS">
        <acl name="MtaJS"></acl>
        <acl name="Admin"></acl> <!-- The most authoritative ACL -->
        <object name="resource.MtaJS"></object>
    </group>
```
We create a new group and add the **Admin** and **MtaJS** ACLs into it.
> The most authoritative ACL should be acl with all privileges. Errors may occur if your server's Admin ACL has been tampered with.

## Step Four
The last step is to add the **Mta JS** script to the **resources** folder.
> *Changing the script name prevents the system from working. Please do not change the name of the script.**

# Create an app
# Step One
The module works by using the accounts as an application. Therefore, an account must be opened for each application.
- [You can create account with code](https://wiki.multitheftauto.com/wiki/AddAccount)
- You can use `addaccount <name> <password>` command to create account with server console. Example: `addaccount TestBot iloveyou`
- You can use the `/register <name> <password>` command in the game.
- If you have a login script, you can create a new account using it.
# Step Two
```xml
    <group name="MtaJS">
        <acl name="MtaJS"></acl>
        <acl name="Admin"></acl> <!-- The most authoritative ACL !-->
        <object name="resource.MtaJS"></object>
        <object name="user.TestBot"></object>
    </group>
```
We add our app to acl.
> If your server is open, you need to renew the acl by typing `reloadacl` in the server console.

# Create First App
```js
const Mta = require('mta.js')
const client = new Mta.Client("serverIP", serverPort);

client.on('ready', _ => {
    client.Initilaze([
        "onPlayerChat"
    ])
})

client.on('onPlayerChat', (player, message, messageType) => {
    console.log(`${player.Name}: ${message}`)
})

client.Login('TestBot', "iloveyou", 1042, false).then(status => {
    console.log(`Listening server on ${client.Http.EndPoints.Port} port.`)
})
```
> **In the Client.Login process, if your application and your server are running on the same machine, set the last value to true.**

> You need to initialize the events you use. **If you don't, your events will not be processed.**

> **You must initiate the initialization when or after the client.ready event is called!**
