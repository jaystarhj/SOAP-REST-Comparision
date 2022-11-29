# SOAP-REST-Comparision
## How to set up


### 1. install packages

navigate to the root of project install all required packages
    
    pip install -r requirements.txt

### 2. change database settings

edit SoapAndRest/settings.py. change database setting

    # Postgresql
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'ws',  # database name
            'USER': 'test',  # username
            'PASSWORD': 'test',  # password
            'HOST': 'localhost',  # server
            'PORT': '5432'  # port
        }
    }

### 3. init database 

    python manage.py makemigrations
    
    python manage.py makemigrations rest

    python manage.py migrate


### 4. start the server

    python manage.py runserver 8000

this will run server at port 8000

### 5. Mock data (only once)
    
    http://127.0.0.1:8000/rest/mock 
    

### 6. you can get all countries via rest now 
    
    http://127.0.0.1:8000/rest/country/all

### 7. SOAP WSDL

    http://127.0.0.1:8000/soap/?wsdl

![wsdl.png](wsdl.png)

### more routes for rest

    GET     http://127.0.0.1:8000/rest/country/1     GET Country info By ID=1
    PUT     http://127.0.0.1:8000/rest/country/1     Update Country info By ID=1
    DELETE  http://127.0.0.1:8000/rest/country/1     delete Country By ID=1
    POST    http://127.0.0.1:8000/rest/country       create new country

### example for SOAP

Make Post Request to get country info by id=1

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:coun="country.soap.ws.api">
       <soapenv:Header/>
       <soapenv:Body>
          <coun:getCountryById>
             <!--Optional:-->
             <coun:country_id>1</coun:country_id>
          </coun:getCountryById>
       </soapenv:Body>
    </soapenv:Envelope>

Response

    <soap11env:Envelope xmlns:soap11env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tns="country.soap.ws.api" xmlns:s0="soap.views">
       <soap11env:Body>
          <tns:getCountryByIdResponse>
             <tns:getCountryByIdResult>
                <s0:country_id>1</s0:country_id>
                <s0:name>Japon</s0:name>
                <s0:capital>Tokyo</s0:capital>
                <s0:currency>JPY</s0:currency>
             </tns:getCountryByIdResult>
          </tns:getCountryByIdResponse>
       </soap11env:Body>
    </soap11env:Envelope>

### How to test
	
install soapUI on your local machine. import the two xml files

	REST-Project-soapui-project.xml
	Soap-Project-soapui-project.xml
	
you will see the results as below

![soapU_test_demo](soapU_test_demo.png)

click the run button, this will run a test case with 100 threads and last 60 seconds.
