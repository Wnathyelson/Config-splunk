Configurando Splunk com Docker Compose:

    - Baixar o documento yml do docker-compose com as configurações do splunk:
        https://www.mediafire.com/file/hiy9dlmqtn987ep/docker-compose.yml/file
    
    - Colocar em um diretório de preferência.

    - Abrir o terminal e executar o seguinte comando:

        sudo docker-compose up -d (no Windows não precisa colocar "sudo").

    - Esse comando acima vai baixar a imagem do splunk com toda configuração definida
    no arquivo do docker compose.

Configurando as dependências do Splunk no projeto:
    
    - No arquivo pom.xml adicione o repositório e as dependências abaixo:
    
    <repositories>
        <repository>
            <id>splunk-artifactory</id>
            <name>Splunk Releases</name>
            <url>https://splunk.jfrog.io/splunk/ext-releases-local</url>
        </repository>
    </repositories>

    <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>
    <dependency>
        <groupId>com.splunk.logging</groupId>
        <artifactId>splunk-library-javalogging</artifactId>
        <version>1.8.0</version>
    </dependency>

Configurando o log4j2:
    
    - Baixar arquivo log4j2-spring.xml com as configurações do splunk:
        https://www.mediafire.com/file/mn3e0g9634a5k7z/log4j2-spring.xml/file

    - Colcoar o arquivo log4j2-spring.xml dentro do diretório resources da aplicação

Entrando no Splunk:

    - Primeiramente deve-se subir a aplicação no servidor
    - No browser acesse: http://localhost:4000/
    - Uma tela de login será exibida, acesse com:
        - user : admin.
        - password: está no docker-compose.yml

Configurando o Token de acesso do Splunk:

    - Depois de entrar no Splunk:
        - Clique em Settings

        - Clique em data inputs: selecione HTTP Event Collector

        - Clique em Global Settings: para desmarcar a opção Enable SSL

        - New Token: Informe o nome do index e o source name da aplicação que está no 
        arquivo log4j2-spring.xml

        - Clique em Next

        - Input Settings:
            -Index: em Select Allowed Indexes, selecione o index especificado na
            etapa anterior de acordo com o que está no arquivo: log4j2-spring.xml
            
            -Source Type: Clique em Select > clique em Select Source Type > Digite: 
            json, e selecione a opção _json
            
        - Clique em Review e em seguida Submit
        
        - Copie o token e cole o mesmo em "token" no arquivo log4j2-spring.xml
        
        - Clique em Start Searching: E para realizar as buscas usamos um modelo de
        query como esse: source="test-api" (index="test-api-idx") sourcetype="_json",
        mas também podemos personalizar: index="test-api-idx"
        
        
        
        
        

    

