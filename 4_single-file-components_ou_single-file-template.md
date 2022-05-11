## **Single File Components** ou **Single File Template**

##### Componente de arquivo único ou Modelo de arquivo único

Basicamente falando, correspondem a menor parte da aplicação front-end. Com suas próprias caracterísitcas e comportamentos.
Ou seja, a ideia é criar pequenas partes de uma aplicação com responsabilidades únicas e de modo bem estruturado. Para que sejam reutilizados em outras partes da aplicação.

### Divisão de um Single File Components

Todo single file component terá 3 pilares:

* ~~~html 
    <template></template> 
    <!-- corresponde a parte visual, ou seja, os elementos html -->
    ~~~

* ~~~html 
    <script>
        // parte lógica do component, onde é possível exportar e importar components ou outros arquivos que o compoẽm.
    </script> 
    ~~~ 
* ~~~html 
    <style>
        /*
        * parte de estilização dos elementos visuais.
        */
    </style>
    ~~~

Todo Single File Component terá a extensão ``` .vue ``` e por convenção o arquivo será denominado com PascalCase.