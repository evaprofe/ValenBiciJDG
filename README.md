# ValenviciJDG

Tarea 1-Crear un proyecto Java llamado ValenbiciAPI  

Para empezar a manejar APIs en Java, vamos a crear un primer proyecto de prueba. En este primer momento, es fundamental que entendáis bien el código. Esta parte consiste en probar el siguiente código, entenderlo y completarlo.  
 

Crea un proyecto de java en NetBeans llamado ValenbiciApi.java con una plantilla de Maven  

Copia el código que te proporcionamos.  

Completa el código para que muestre la estación, las bicicletas disponibles y espacios disponibles.  

  

//valenbiciAPIv1.java  


package es.gva.edu.iesjuandegaray.bicis;  

import org.apache.http.HttpEntity;  

  

import org.apache.http.HttpResponse;  

import org.apache.http.client.methods.HttpGet;  

import org.apache.http.impl.client.CloseableHttpClient;  

import org.apache.http.impl.client.HttpClients;  

import org.apache.http.util.EntityUtils;  

import org.json.JSONArray;  

import org.json.JSONObject;  

  

import java.io.IOException;  

  

public class ValenbiciAPI {  

    private static final String API_URL = "https://valencia.opendatasoft.com/api/explore/v2.1/catalog/datasets/valenbisi-disponibilitat-valenbisi-dsiponibilidad/records?limit=20";  

  

    public static void main(String[] args) {  

        if (API_URL.isEmpty()) {  

            System.err.println("La URL de la API no está especificada.");  

            return;  

        }  

  

        try (CloseableHttpClient httpClient = HttpClients.createDefault()) {  

            HttpGet request = new HttpGet(API_URL);  

            HttpResponse response = httpClient.execute(request);  

  

            HttpEntity entity = response.getEntity();  

            if (entity != null) {  

                String result = EntityUtils.toString(entity);  

                System.out.println("Respuesta de la API:");  

                System.out.println(result);  

  

                // Intentamos procesar la respuesta como JSON  

                try {  

                    JSONObject jsonObject = new JSONObject(result);  

                    JSONArray resultsArray = jsonObject.getJSONArray("results");  

  

                    // Recorre el vector resultsArray mostrando los datos solicitados.  

  

  

  

  

  

                } catch (org.json.JSONException e) {  

                    // Si la respuesta no es un array JSON, imprimimos el mensaje de error  

                    System.err.println("Error al procesar los datos JSON: " + e.getMessage());  

                }  

            }  

        } catch (IOException e) {  

            e.printStackTrace();  

        }  

    }  

}  

 

Tarea 2-Configurar el archivo pom.xml  

  

Ahora, como hemos utilizado una plantilla de Maven, deberás configurar el archivo pom.xml que se encuentra en los ficheros de tu proyecto Java en NetBeans.   

  

¿Cómo funciona Apache Maven?  

  

Maven usa un modelo de objetos de proyecto (POM) para administrar un proyecto.  

  

Los comandos de Maven ejecutan partes de su modelo de objetos de proyecto. Un modelo de objetos de proyecto se suele describir como un documento XML. Una descripción de POM NO se limita a XML.  

  

Se pueden utilizar otros formatos para describir el modelo de objetos del proyecto, sin embargo, XML fue el primer formato utilizado.  

Diagrama

El contenido generado por IA puede ser incorrecto.  

Modelo de objeto del proyecto  

The Project Object Model  

The Project Object Model  

  

¿Qué es el archivo POM?  

  

Archivo XML que contiene información relevante del proyecto.  

El POM Maven dice qué tipo de proyecto se está trabajando y cómo modificar el comportamiento por defecto para generar la salida.  

  

  

  
 

Abrir el archivo pom.xml desde NetBeans situado aquí:  

  

Interfaz de usuario gráfica, Texto, Aplicación, Chat o mensaje de texto

Descripción generada automáticamente  

  

Y copiar la siguiente configuración a pom.xml   

  

<?xml version="1.0" encoding="UTF-8"?>  

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  

    <modelVersion>4.0.0</modelVersion>  

    <groupId>JDE</groupId>  

    <artifactId>ValenbiciAPI</artifactId>  

    <version>1.0-SNAPSHOT</version>  

    <packaging>jar</packaging>  

    <properties>  

        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  

        <maven.compiler.release>23</maven.compiler.release>  

        <exec.mainClass>jde.valenbiciapi.ValenbiciAPI</exec.mainClass>  

    </properties>  

    <dependencies>  

        <dependency>  

            <groupId>org.apache.httpcomponents</groupId>  

            <artifactId>httpclient</artifactId>  

            <version>4.5.13</version>  

        </dependency>  

        <dependency>  

            <groupId>org.json</groupId>  

            <artifactId>json</artifactId>  

            <version>20210307</version>  

        </dependency>  

    </dependencies>  

    <build>   

        <plugins>   

            <plugin>   

                <groupId>org.codehaus.mojo</groupId>   

                <artifactId>exec-maven-plugin</artifactId>   

                <version>3.1.0</version>   

                <configuration>   

                    <mainClass>es.gva.edu.iesjuandegaray.bicis.ValenbiciAPI</mainClass>   

                </configuration>   

            </plugin>   

        </plugins>   

    </build>  

</project>  

  

Revisa el código fijándote en las dependencias creadas,artefactos y plugins , ejecuta el programa Java y te darás cuenta de que se han recogido algunos datos provenientes de la API ValenBici .  

 
