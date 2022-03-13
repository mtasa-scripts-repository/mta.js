# Installing
Modülün kurulumu sırasında yapılması gerekli olan adımları içerir.
## Step One
MTA sunucusunun **acl.xml** dosyasına birkaç küçük ekleme yapacağız.

```xml
<acl name="Default">
   <right name="resource.MtaJS.http" access="false"></right>
</acl>
```
Default isimli acl'ye yeni bir kural ekleyeğiz.
Bu kural **yetkilendirme** için oldukça önemlidir.
> Bu Kuralı eklemezseniz herkes sistemi kullanabilir ve sunucunuza tam erişim izni alabilir!

## Step Two
```xml
<acl name="MtaJS">
   <right name="function.fetchRemote" access="true"></right>
   <right name="resource.MtaJS.http" access="true"></right>
</acl>
```
Yeni bir acl oluşturacağız ve adını **MtaJS** koyacağız. İçerisine iki tane kural ekliyoruz.<br>
> Bu kurallar sunucu ile istemci arası iletişimi sağlamaktadır.

## Step Three
```xml
    <group name="MtaJS">
        <acl name="MtaJS"></acl>
        <acl name="Admin"></acl> <!-- En Yetkili ACL !-->
        <object name="resource.MtaJS"></object>
    </group>
```
Yeni bir grup oluşturuyoruz ve içerisine **Admin** ve **MtaJS** ACL'lerini  ekliyoruz.
> En yetkili ACL, tüm yetkilerin olduğu acl olmalıdır. Eğer sunucunuzun Admin ACL'si oynanmış ise hatalar oluşabilir.

## Step Four
Son adım, **resources** klasörüne **MtaJS** scriptini ekliyoruz.
> **Script adını değiştirmek, sistemin çalışmasını engellemektedir. Lütfen scriptin adını değiştirmeyiniz.**

# Add an app
# Step One
Modül, hesapları uygulama gibi kullanarak çalışmaktadır. Bu yüzden her uygulama için bir hesap açılmalıdır.
- [Kod ile hesap oluşturabilirsiniz](https://wiki.multitheftauto.com/wiki/AddAccount)
- Sunucu konsolu ile hesap oluşturmak için `addaccount <name> <password>` kullanabilirsiniz. Örnek: `addaccount TestBot iloveyou`
- Oyunda `/register <name> <password>` komudunu kullanabilirsiniz.
- Eğer login scriptiniz var ise onu kullanarak yeni hesap oluşturabilirsiniz.
# Step Two
```xml
    <group name="MtaJS">
        <acl name="MtaJS"></acl>
        <acl name="Admin"></acl> <!-- En Yetkili ACL !-->
        <object name="resource.MtaJS"></object>
        <object name="user.TestBot"></object>
    </group>
```
Uygulamamızı acl'ye ekliyoruz.
>  Eğer sunucunuz açık ise sunucu konsoluna `reloadacl` yazarak acl'yi yenilemeniz gerekmektedir.

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
> **Client.Login işleminde uygulama ile sunucunuz aynı makinada çalışıyorsa en sondaki değeri true olarak ayarlayınız.**

> Kullandığınız eventleri Initilaze etmeniz gerekmektedir. **Yapmazsanız eventleriniz işlenmez.**

> **Initilaze işlemini client.ready eventi çağrıldığında veya çağrıldıktan sonra yapmalısınız!**
