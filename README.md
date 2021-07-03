# SQLitedatabase
## Veri tabanıyla ilgili işlemler yaparken try-catch blokları arasında yazmamız gerekmektedir. Çünkü burda SQL komutları yazacağız. Burda oluşturacağımız veritabanı herkesin local cihazında saklanır.<br>
- SQLiteDatabase sınıfından bir nesne üretiyoruz. Ve openOrCreateDatabase() metodulanarak veritabanımızı oluşturuyoruz.<br>
- Bir veritabanını excel gibi düşünebiliriz. Row ve columnları vardır.<br>
- Bunun için önce tablo oluşturmamız gerekmektedir.<br>
- "CREATE TABLE IF NOT EXISTS" bir tablo oluştur eğer yoksa.<br>
````
SQLiteDatabase database=this.openOrCreateDatabase("Musicians",MODE_PRIVATE,null);
database.execSQL("CREATE TABLE IF NOT EXISTS musicians (name VARCHAR,age INTEGER)");
````
<br>
- Oluşturulan bu tabloya veri eklerken "INSERT INTO tablo adı (kolonların adı) VALUES (değerleri)" kullanılır.Değerleri kısmında string ifade '(tek tırnak) ' içine yazılmalıdır. <br>

````
 database.execSQL("INSERT INTO musicians (name,age) VALUES ('James',50)");
 ````

## Verileri listelemek ve kullanmak için Cursor(imleç) dediğimiz sınıfa ihtiyacımız var.
 - Sırayla veritabanımızı, tablomuzu ve columları oluşturduk. Sonra içerisine değer ekledik. Şuan eklenen değerleri çekmemiz gerekmektedir. 
 Cursor tek tek hücrelerin içerisinde geziyor ve bize verileri aktarıyor.
 - rawQuery() sorgu yazılması için kullanılır.musicians içindeki herşeyi çek. , filtreleme istiyor musunuz diye soruyor.<br>
 - Cursora hangi sütunlara gideceğimizi söylememiz gerekiyor.
 bizim sutunlarımızda name ve age var.<br>
 - getColumnIndex() kaçıncı sütunda olduğunu verecek. <br>
 - moveToNext() - cursor bütün verileri ilerleyebildiği kadar gidecek tek tek gezecek. O sırada bizim yapmak istediğim şey ise değerleri okumak 
 işlem bittikten sonra cursor ı kapatacağım. <br>
-```
        Cursor cursor=database.rawQuery("SELECT * FROM musicians",null);

            int nameIx=cursor.getColumnIndex("name");
            int ageIx=cursor.getColumnIndex("age");

            while(cursor.moveToNext()){
                System.out.println("Name: "+cursor.getString(nameIx));
                System.out.println("Age: "+cursor.getInt(ageIx));

            }
            cursor.close();

-```
## Veritabanı oluşturma veri ekleme ve gösterme aşaması: <br>
![metin](https://github.com/isilay-subasi/SQLitedatabase/blob/main/images/SQLiteCreate.PNG)
<br>
## FİLTRELEME<br>
-<b> "SELECT * FROM musicians WHERE id=2"<b> idsi 2 olanları getir anlamına gelmektedir.<br>
 - "SELECT * FROM musicians WHERE name='James'" name i James olanları getir anlamındadır.
 <br>
 - database.execSQL("UPDATE musicians SET age=89 WHERE name= 'Lars'");  ismi Lars olan kişinin yaşını 89 olarak değiştir. Güncelleme yapmış olduk.
 <br>
 -  database.execSQL("DELETE FROM musicians WHERE id=2"); id'si 2 olanı sil.
  <br>
  - Cursor cursor=database.rawQuery("SELECT * FROM musicians WHERE name LIKE '%s'",null); LIKE %s sonu s harfi ile bitenleri getir demektir.















