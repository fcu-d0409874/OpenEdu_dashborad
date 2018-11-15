# OpenEdu_dashborad


# 簡介
  將以JAVA為基底的網頁架構，改寫成使用以Python為基底的web應用框架-Django開發網頁，配合MySQL作為資料庫，並且增加新功能，最後上架至docker的伺服器之中。
  

## 環境配置
  
  python3.6版本、django2.0.6、MySQL5.7、
  
  docker:
  
    Client:
    Version:           18.06.1-ce  
    API version:       1.38  
    Go version:        go1.10.3  
    Git commit:        e68fc7a  
    Built:             Tue Aug 21 17:24:56 2018  
    OS/Arch:           linux/amd64

# Django介紹
  Django是一種採用MVT軟體設計模式的網頁開發框架，即model、view、template。
  
  在python的環境底下輸入指令pip install django即可安裝。
  之後便可以輸入django-admin.py startproject XXX指令便會在指定的XXX資料夾創建專案。
  然後便可以在其中找到setting.py這個檔案，使用其將許多配置在其中設定完成。
  如app的配置、database詳細資料的配置、static(靜態檔案如CSS、img)及template(模板html)的位置。
  
  ### Database
  django支援非常多種的DataBase，而我們選擇使用MySQL5.7版本，在setting.py中設定好資料庫的連線設定後就可以直接連上資料庫提取使用。
  
### template
  django版本的html所使用的語法和jsp版本所使用的有些許不同:
  
  
| JSP | Django  |
| :------------ |:---------------|
| 包含其他的template <br /> <%@ include file='sidebar.html' %>| {% include 'sidebar.html' %} |
| <c:forEach var="a" items=”b"}> <br />&emsp;.... <br /> </c:forEach>| {% for a in b %} <br /> &emsp; ... <br /> {% endfor %} |
| <c:set <br /> var="&lt;string>" <br /> value="&lt;string>" <br /> target="&lt;string>" <br /> property="&lt;string>" <br /> scope="&lt;string>"/>  | {% with value as var %}<br />{% endwith %}|
| <c:if test="&lt;boolean>" var="&lt;string>" scope="&lt;string>"><br />&emsp;...<br /></c:if> | {% if a %}<br />&emsp;...<br />{% elif %}<br />&emsp;...<br />{% else %}<br />&emsp;...<br />{% endif %} |
| <c:choose> <br /> &emsp;<c:when test="&lt;boolean>"> <br />&emsp;&emsp; ... <br />&emsp; </c:when> <br />&emsp;<c:when test="&lt;boolean>"><br />&emsp; ... <br />&emsp; </c:when><br /> &emsp;... <br />&emsp; <c:otherwise><br /> &emsp;...<br />&emsp; </c:otherwise> <br /> </c:choose> | 沒有這種類似swith case的寫法，所以直接沿用上方的if else來重新編寫達成同樣效果。 |
  
