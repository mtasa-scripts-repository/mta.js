# Installing
Modülün kurulumu sırasında yapılması gerekli olan adımları içerir.
## Step one
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
