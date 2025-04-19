
En esta ocasion resolveremos el laboratorio -> Tomcat Takeover Lab

empezamos extrayendo el comprimido, con la contraseña proporcionada

![zip](assets/images/2025-04-19_10-56.png)

nos deja un archivo pcap, por lo cual lo analizamos con wireshark

<img src="https://private-user-images.githubusercontent.com/206333974/435410877-b5fb54d7-28a4-4cae-83ca-26c23556d258.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwODI0NjMsIm5iZiI6MTc0NTA4MjE2MywicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDEwODc3LWI1ZmI1NGQ3LTI4YTQtNGNhZS04M2NhLTI2YzIzNTU2ZDI1OC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNzAyNDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03MGRhZjk1ZWU2Y2VlYWI2Y2QwOTdlNWRmODYxYmZiNTE5NGNhMTBjMjYzODFhZTkyNzRhZjlkNmJkM2RmNWVlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ziVTvIuSGTiAuu44bY3kvuODIeeWl3AI_0172CtlVmg" width="600" />


Q1: Dada la actividad sospechosa detectada en el servidor web, el archivo PCAP revela una serie de solicitudes en varios puertos, lo que indica un posible comportamiento de escaneo. ¿Puede identificar la dirección IP de origen responsable de iniciar estas solicitudes en nuestro servidor?


Si nos vamos a "Conversations" en Wireshark podemos indentificar facilmente como la ip del atacante es --> 14.0.0.120  el cual ejecuta un escaneo por tcp a multiples puertos del host 10.0.0.112 

<img src="https://private-user-images.githubusercontent.com/206333974/435401953-e0f89961-695d-46c1-ad8d-597eb5cedd67.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzQ5MzYsIm5iZiI6MTc0NTA3NDYzNiwicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDAxOTUzLWUwZjg5OTYxLTY5NWQtNDZjMS1hZDhkLTU5N2ViNWNlZGQ2Ny5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNDU3MTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NTY3MjA4MTE3MDI5MTE1YzYyNjhhYzlkMmUxOGEzYzczZmJiNDJmZjg1NTdkZWUxZTE3YjAyNDI4OGI4ZGQyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.TZTbCq7PoW-uZDOUB3gAdRvleQ1arNisScEab93pwMk" width="1000" /> 

-------------------



Q2: Según la dirección IP identificada asociada con el atacante, ¿puede identificar al país desde el cual se originaron las actividades del atacante?

al investigar la IP nos muestra que Proviene de China


<img src="https://private-user-images.githubusercontent.com/206333974/435402924-f44708e2-cb28-4e92-a333-f2b3392ffa97.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzU1ODcsIm5iZiI6MTc0NTA3NTI4NywicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDAyOTI0LWY0NDcwOGUyLWNiMjgtNGU5Mi1hMzMzLWYyYjMzOTJmZmE5Ny5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNTA4MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02NjA3YWNlY2IzNjFjNGI0NDE2MTYwNTA3ZmY5ODk0NzM1MjhhYWEzNjBlNTg1YjkxMTEwMjJkMThkZDM4ZDY1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.sSOpN_ub6b5WA82lRZOMxBMfrzZeWVkdTwgMwHBD1xA" width="900" />

--------------------

Q3: Entre los diversos puertos abiertos detectados durante el escaneo, uno proporciona acceso al panel administrativo del servidor web. ¿Qué número de puerto corresponde al panel de administración?

si filtramos por el trafico http y la IP del atacante en Wireshark podremos ver que se accede a la ruta '/Manager' la cual es por defecto el panel de administracion del servidor Tomcat, alojada en el Puerto: 8080


<img src="https://private-user-images.githubusercontent.com/206333974/435404638-7f4d7d02-2fd9-4045-99e8-05929f594612.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzY3NjAsIm5iZiI6MTc0NTA3NjQ2MCwicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA0NjM4LTdmNGQ3ZDAyLTJmZDktNDA0NS05OWU4LTA1OTI5ZjU5NDYxMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNTI3NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lNTRmNzIyNGVlOGY3NzVjYjdhNzBjYTk2NGQ3ODg2MmJiOWJjNDUyOTgxZDY5OTM0ZTg2MTdkZmY5NjQ1NzhmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.3M3wKcNqFiaIctarNODR4hlI65MmUcqsKA1ZyHHCb_U" width="900" />

--------------

Q4: Después del descubrimiento de puertos abiertos en nuestro servidor, parece que el atacante intentó enumerar y descubrir directorios y archivos en nuestro servidor web. ¿Qué herramientas puede identificar del análisis que ayudó al atacante en este proceso de enumeración?


Filtrando por la IP del atacante y por codigos de estado 404, veremos multiples solicitudes por fuerza bruta, a directorios que no existen. nos vamos a Follow TCP Stream, y miramos el user-agent, el cual no fue alterado y revela el uso de la herramienta gobuster

<img src="https://private-user-images.githubusercontent.com/206333974/435406012-2d53cbf0-0a6e-4f27-9782-862ddfbce1fa.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzc4NjcsIm5iZiI6MTc0NTA3NzU2NywicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA2MDEyLTJkNTNjYmYwLTBhNmUtNGYyNy05NzgyLTg2MmRkZmJjZTFmYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNTQ2MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wMmIyZGVhZjYwOWEyNTIwZDc1MzFjYzM5ZDE3NDY1NzMyMDc4Yzc1YmNmMTEyNzI0ZmM4MWY0YzdiMDljYzk0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.zTMqZuytCFIoLBNWiQAGwfTg2cC1tvli64OjKIdxPCI" width="1000" />

----------


Q5: Después del esfuerzo por enumerar los directorios en nuestro servidor web, el atacante realizó numerosas solicitudes para identificar interfaces administrativas. ¿Qué directorio específico relacionado con el panel de administración descubrió el atacante?


En este caso filtraremos por codigos de respuesta 200, si analizamos, podremos ver que el atacante accede a la ruta '/Manager' la cual como dijimos anteriormente, sabemos que es la ruta del panel de administración.


<img src="https://private-user-images.githubusercontent.com/206333974/435406940-7ba36267-af63-485b-b78c-60407af3fa06.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzg5NjIsIm5iZiI6MTc0NTA3ODY2MiwicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA2OTQwLTdiYTM2MjY3LWFmNjMtNDg1Yi1iNzhjLTYwNDA3YWYzZmEwNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNjA0MjJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05OTAyYmJhZjA1NWMyNjhlZjU0MzJiY2YzY2E3ZGQ2ZmQ3YTRjZGI5YmQ2ZmU4Yzc1OTQwOGI1OWZlMDQwMjAwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.mBTj8vZacLYxVNk96JFslEaYiMPS-jjKhKrRYevOvXg" width="1000" />

----------

Q6: Después de acceder al panel de administración, el atacante intentó hacer fuerza bruta a las credenciales de inicio de sesión. ¿Puede determinar el nombre de usuario y la contraseña correctos que el atacante usó con éxito para iniciar sesión?


Para determinar las credenciales de acceso, tendremos que filtrar por: ```http.request.method == POST``` 
`POST` es uno de los **métodos HTTP** usados para enviar datos desde el cliente (como un navegador o herramienta) al servidor. Una vez aplicado el filtro podremos ver las credenciales  admin:tomcat

<img src="https://private-user-images.githubusercontent.com/206333974/435408077-02e29428-5bd8-4d0d-a922-e79d248153da.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwNzk4NDMsIm5iZiI6MTc0NTA3OTU0MywicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA4MDc3LTAyZTI5NDI4LTViZDgtNGQwZC1hOTIyLWU3OWQyNDgxNTNkYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNjE5MDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mNmM2NzdhNmQzNDc1NGI0MjZiOGE4N2M0NWZjM2M4Y2YxNTY2MzdjYmJkMDAxZTllYTUxMTg3YzRlMTdlOWE3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZcDdX1rBTHefZruRaE4_tsDxVELPPwq5asIkPHeAc9g" width="900" />

--------------

Q7: Una vez dentro del panel de administración, el atacante intentó cargar un archivo con la intención de establecer un shell inverso. ¿Puede identificar el nombre de este archivo malicioso?


En el mismo paquete, veremos el archivo que se sube un archivo con el nombre: "JXQOZY.war"

<img src="https://private-user-images.githubusercontent.com/206333974/435408546-383d0d79-1cd5-4a0a-bd2c-4ad821b4d0d4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwODAzMDYsIm5iZiI6MTc0NTA4MDAwNiwicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA4NTQ2LTM4M2QwZDc5LTFjZDUtNGEwYS1iZDJjLTRhZDgyMWI0ZDBkNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNjI2NDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xZTg3MWY2YmZhMjZjYTM1MTYwMTFhYzIyOGI1MzRkNTcwMDQ2Zjk2OGYxNDE4YWYyZGFlZjA1YWYwZTY2NzZiJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.-4fvyNwla-_r4J7x1GlMP5PP-bjMo7weaFCzTh_wTrE" width="1000" />

-----------

Q8: Después de establecer con éxito un shell inverso en nuestro servidor, el atacante tuvo como objetivo garantizar la persistencia en la máquina comprometida. Del análisis, ¿puede determinar el comando específico que están programados para ejecutar para mantener su presencia?

Podremos ver mediante TCP Stream, que la siguiente acción del atacante es acceder a este recurso, el cual el contenido es una típica reverse shell de bash

<img src="https://private-user-images.githubusercontent.com/206333974/435409183-9ccfc764-786e-498f-96d6-2ff89a4b5fb3.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDUwODA5MDUsIm5iZiI6MTc0NTA4MDYwNSwicGF0aCI6Ii8yMDYzMzM5NzQvNDM1NDA5MTgzLTljY2ZjNzY0LTc4NmUtNDk4Zi05NmQ2LTJmZjg5YTRiNWZiMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQxOVQxNjM2NDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wODA3MzIwZjBhMmM0ODlmNDYyNjhkNjBmOGRlYjMyMzNkODQ1ODZhNjZiNmI5YzdiNDE1ZDUxYzRmMTRkZTY1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.1Aw4S2wI9QIDo_N9uGlc171n6pq6kiJoocAsAxUdF1s" width="900" />
