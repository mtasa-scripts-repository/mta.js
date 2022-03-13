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
