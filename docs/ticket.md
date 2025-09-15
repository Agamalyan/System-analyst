
Название - Фильтрация списка фильмов и сериалов по эксклюзивности  
Цель - Увеличить аудиторию сервиса за счет возможности просмотра эксклюзивных категорий фильмов и сериалов  
Требование - Иметь возможность отфильтровать весь список фильмов и сериалов, которые представлены в Otium по признаку эксклюзивности.  

UseCase:
1. В разделе «Библиотека» пользователь выбирает чек-бокс «представлены эксклюзивно в Otium».
2. UI запрашивает список фильмов и сериалов по выбранным параметрам.
3. API возвращает список фильмов и сериалов, которые представлены
4. Пользователь выбирает нужный фильм из представленного списка

Описание изменений:  
Необходимо доработать метод POST {{WebServer}}/content/list Web Server API:
1. Добавить параметр запроса «exclusive» с типом “boolean”
2. Добавить параметр «exclusive» с типом “boolean” в тело ответа
3. если exclusive=true, то в ответе должен возвращаться только тот контент, у которого поле exclusive=true,
если exclusive=false, то в ответе должен возвращаться весь контент, эксклюзивный и неэксклюзивный
Контекст - В ответе запроса {{FilmsServer}}/films/list и {{SeriesServer}}/series/list уже есть элемент «exclusive». 


XML-схема GetContentListRequest.xsd  
<pre>
<?xml version="1.0" encoding="UTF-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
 <xs:element name="GetContentList">]  
  <xs:complexType>  
   <xs:sequence>  
    <xs:element name="contentType" type="xs:string" />  
    <xs:element name="genreValue"  type="xs:string" />  
    <xs:element name="exclusive" type="xs:boolean"   />  
   </xs:sequence>  
  </xs:complexType>  
 </xs:element>  
</xs:schema>  
</pre>

XML-схема GetContentListResponse.xsd
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://www.w3.org/2003/05/soap-envelope/" soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding"
>
<xs:element name="GetContentListResponse">
<xs:complexType>
<xs:sequence>
<xs:element name="contentList">
<xs:complexType>
<xs:sequence>
<xs:element name="content">
<xs:complexType>
<xs:sequence>
<xs:element name="contentType" type="xs:string" />
<xs:element name="contentId" type="xs:intr" />
<xs:element name="title" type="xs:string" />
<xs:element name="description" type="xs:string" />
<xs:element name="imageUrl" type="xs:string" />
<xs:element name="previewUrl" type="xs:string" />
<xs:element name="recordUrl" type="xs:string" />
<xs:element name="genre type="xs:string" />
<xs:complexType
<xs:sequence>
<xs:element name="genreValue" type="xs:string" />
</xs:sequence>
</xs:complexType>
<xs:element name="recommended" type="xs:boolean" >
<xs:element name="exclusive"  type="xs:boolean" >
<xs:element name="details" >
<xs:complexType>
<xs:sequence>
<xs:element name="yearOfIssue" type="xs:string" />
<xs:element name="duration" type="xs:string” />
<xs:element name=”country” >
<xs:complexType>
<xs:sequence>
<xs:element name="countryValue" type="xs:string" maxOccurs="5" />
</xs:sequence>
</xs:complexType>
<xs:element name="ageRate"  type="xs:string" />
</xs:sequence>
</xs:complexType>
</xs:element>
<xs:element name="team">
<xs:complexType>
<xs:sequence>
<xs:element name="cast">
<xs:complexType>
<xs:sequence>
<xs:element name="castValue" type="xs:string" />
</xs:sequence>
</xs:complexType>
</xs:element>
<xs:element name="dubbingTeam" type=”xs:string" />
</xs:sequence>
</xs:complexType>
</xs:element>
<xs:element name="rating" type="xs:decimal"/>
</xs:sequence>
</xs:complexType>
</xs:element>
</xs:sequence>
</xs:complexType>
</xs:element>
</xs:sequence>
</xs:complexType>
</xs:element>
</xs:schema>



