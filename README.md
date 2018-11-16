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
|引用變數 <br /> ${var[int]} | {{var.int}} |
| &lt;li>&lt;a href="BeforeSurveyServlet">課前問卷資料</a></li> | &lt;li>&lt;a href="{% url 'BeforeSurveyServlet_instructor'%}">課前問卷資料</a></li> |
| 引入靜態文件時，如圖片、css檔直接寫入 href="target"，target是目標路徑，由jsp的所在位置直接去搜索 | html開頭必須設置 {% load static %}，"{% static '目標位置' %} |

### url

### view
  django的view是用來將資料傳入templates中的html檔
  
| Java | Django  |
| :------------ |:---------------|
| 處理request的請求時，是用doGet()、doPost分別去處理GET、與POST| 在view中使用if request.method=='GET': 及 if request.method=='POST':來區分|
| 處理資料庫連接時需自行設定大量程式碼，如：<br/>MysqlDataSource mysqlDS = new MysqlDataSource() <br/>protected DataSource getDataSource() <br/>MysqlDataSource mysqlDS = new MysqlDataSource();<br/> mysqlDS.setURL(......) <br/> mysqlDS.setUser(......) <br/> mysqlDS.setPassword(......) <br/> return mysqlDS<br> 隨後在java檔中宣告Connection該類別進行連接 | 在主目錄中的setting.py中設定DATABASES這一dictionary，如下：<br/> 'ForExample': {<br/>&emsp;&emsp;'ENGINE': 'django.db.backends.mysql',<br>&emsp;&emsp;'NAME': 'edxresult',<br>&emsp;&emsp;'USER': 'xxx',<br>&emsp;&emsp;...<br>}<br>之後僅需要在view中import django.db.connections後，再利用with connections['ForExample'].cursor() as cursor:後即可進行連接|使用request.setAttribute('XXX', XX)來設定回傳回jsp的屬性，並且使用<br>RequestDispatcher rd = request.getRequestDispatcher("1_BasicCourseData.jsp")來設定要傳給哪個jsp|可自行宣告一個dictionary來存放要回傳的屬性，如：<br>to_render['test']=123<br?隨後利用<br>return render(request, 'test.html', to_render)來決定傳給哪個html|
