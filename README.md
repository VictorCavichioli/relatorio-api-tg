# **Victor Araujo Paula Cavichioli**

## **Introdução**

Olá, seja bem-vindo. Sou o Victor Cavichioli, estudante de **Banco de Dados** pela FATEC Prof. Jessen Vidal. 

Tenho 19 anos e trabalho com DevOps. <br/>

<img src="https://avatars.githubusercontent.com/u/79488234?v=4"/>

<h4><details>
<summary>Meus principais conhecimentos</summary>

#### **Python**

Python foi a primeiras linguagem que estudei, no primeiro semestre da graduação. Hoje como DevOps minhas principais atribuições são utilizando python, pela Fatec também
já fiz um projeto em Python de um assistente virtual, no meu trabalho utilizamos Python para integrar outros serviços, realizar operações de verificação no cluster e
no **Banco de Dados**.

#### **Java**
Java foi a terceira linguagem de programação que aprendi, antes de trabalhar com Python eu trabalhei uma pouco na parte de Billing, e muitos dos serviços são feitos em Java utilizando Spring Boot, juntando isso com os APIs na Fatec que foram em Java, agrego muito valor quando estamos falando em Java e principalmente REST APIs.

#### **Docker**

#### **Kubernetes**

#### **Helm**

#### **Cassandra**

#### **Testes**

</details></h4>

#### **Projetos Integradores durante a graduação**
Durante a minha gradução, trabalhei no desenvolvimento de trabalhos chamados de "Projetos integradores". Um projeto integrador tem o objetivo de solucionar um problema do mundo real, utilizando os conhecimentos adquiridos durante a graduação.<br/>
Abaixo todos estes projetos serão descritos, detalhando o problema, solução proposta (e entregue), e os aprendizamos extraídos de cada um deles.

<h4><details>
<summary>Projeto 1: 1º Semestre de 2021</summary>

### **Parceiro Acadêmico**
Fatec

### **Objetivo do Projeto**

Projeto consistia em criar uma assistente virtual feito em python. Entre os requisitos estão:
  - Responder a comando de voz ou sons específicos (palma, estalar de dedos, etc.); 
  - Possuir no mínimo 8 ações distintas e de natureza distintas; 
  - Ser mobile, web ou desktop; - Retornar o comando em qualquer forma (som, texto ou ação); 
  - Ter um contexto específico de aplicação; 
  - Não pode usar 100% de APIs prontas e disponíveis no mercado, seja gratuita ou não; 
  - Não pode utilizar de plataforma de implementação de terceiros, seja gratuita ou não;

### **Tecnologias adotadas na solução**

### **Banco de Dados**: SqLite
Embora não fosse requisito, utilizamos o SqLite para guardar informações de comparação e quando vamos
realizar uma consulta ou uma comparação, é feito uma query no Banco.

### **Back-end**: Python
Para relização da API utilizamos a linguagem Python, com algumas bibliotecas, são elas:
 - speech_recognition (Para reconhecimento de voz);
 - pyttsx3 (Para síntese de texto em voz);
 - requests (Para realizar requisições na web);
 - BeautifulSoup (Para analisar documentos HTML);
 - Sqlite (Para criar um **Banco de Dados** local).

### **Ferramentas**: PyCharm, Visual Studio Code, GitHub e Figma

### **Contribuições pessoais**
- Funções que reconhecem voz e transformam em texto;

    ```python
    reproducao = pyttsx3.init()

    def sai_som(mensagem, imprimir=True):
        if imprimir:
            print(mensagem)
        reproducao.say(mensagem)
        reproducao.runAndWait()
    ```
    Essa função basicamente recebe uma mensagem e reproduz ela usando a voz do google, se imprimir receber True,
    a mensagem é escrita no chat. Como ela é genérica, foi usada em basicamente todos os arquivos do projeto.

    <details>

    ```python
    def assistente():
        sai_som('Oi, qual é o seu nome?')
        user_name = ''
        
        while True:
            resposta_erro_aleatoria = choice(lista_erros)
            rec = sr.Recognizer()

            with sr.Microphone() as s:
                rec.adjust_for_ambient_noise(s)

                while True:
                    try:
                        audio = rec.listen(s)
                        user_name = rec.recognize_google(audio, language ='pt') 
                        break
                    except sr.UnknownValueError:
                        sai_som(resposta_erro_aleatoria)
                break
    ```
    </details>
    Aqui temos a primeira parte da matriz do assistente, o que estou dizendo aqui primeiramente é que vamos armazenar
    a informação dita pelo microfone na variável 'user_name', que utilizaremos em toda a execução.

    <details>

    ```python
    rec = sr.Recognizer()
    
    with sr.Microphone() as s:
        rec.adjust_for_ambient_noise(s)
        sair = False
        while not sair:
            menu(user_name)
            try:
                resposta_erro_aleatoria = choice(lista_erros)
                audio = rec.listen(s)
                entrada = rec.recognize_google(audio, language ='pt')
                print('{}: {}'.format(user_name, entrada))

                #Funções
                if '<funcionalidade_desejada>' in entrada:
                    entrada = entrada.replace('<funcionalidade_desejada>',' ')
                    resposta = <funcionalidade_desejada>()
                    
                    sai_som('{}'.format(resposta))       
   
                if 'sair' in entrada:
                    sair = True
                                                                
            except sr.UnknownValueError:
                sai_som(resposta_erro_aleatoria)
    ```
    Aqui temos o coração da operação, o usuário é levado a um menu que mostra as funcionalidades implementadas
    e ele terá de escolher uma, para cada função executamos basicamente o mesmo bloco if abaixo:

    ```python
    if '<funcionalidade_desejada>' in entrada:
        entrada = entrada.replace('<funcionalidade_desejada>',' ')
        resposta = <funcionalidade_desejada>()
        
        sai_som('{}'.format(resposta)) 
    ```
    </details>
    Todas as funcionalidades foram divididas em arquivos separados e importadas na matriz e chamadas quando a entrada era 
    igual a flag que atrelamos a ela.
<br/>

- Requisição e interpretação de dados vindos da web;

    <details>

    ```python
    requisição = requests.get('https://economia.awesomeapi.com.br/all')

    cotação = requisição.json()
    def cotacao():
        sai_som('''
            Bem-vindo(a) a cotação do dia!
            Atualmente temos o valor atual das seguintes moedas:
            Dólar - Euro - Libra e Bitcoin!
        ''')
        sai_som('Qual a moeda que deseja cotação?: ')
        Valor_moeda = str(input('')).strip().upper()

        if Valor_moeda == '<moeda_desejada>':
            sai_som('Cotação do Dolar')
            sai_som('Moeda: ' + cotação ['<moeda_desejada_sigla>'] ['name'])
            sai_som('Data: ' + cotação ['<moeda_desejada_sigla>'] ['create_date'])
            sai_som('Valor Atual R$: ' + cotação ['<moeda_desejada_sigla>']['bid'])
    ```
    </details>
    Aqui basicamente estamos primeiramente coletando os valores de cotação e passando para formato json,
    e de acordo com o input do usuário, retornando as informações da moeda.
<br/>

- Tratamento de erro.

    <details>

    ```python
    lista_erros = [
        'Não entendi nada, repita',
        'Esse erro me custou R$0,97 centavos',
        'Sempre que você errar a fala\n EU VOU ESTAR LÁ\n'

    ]

    conversas = {
        'Olá' : 'Oi, tudo bem?',
        'Tudo, e você?' : 'Estou bem, obrigado'

    }

    comandos = {
        'Desligar' : 'Desligando',
        'Reiniciar' : 'Reiniciando'

    }
    ```
    </details>
    Primeiramente para tratar os erros eu defini algumas configurações no arquivo config.py, para padronizar
    retorno de erros, fazendo com que retornasse o valor de erro e o assistente falar uma frase típica.
    ```python
    except sr.UnknownValueError:
        sai_som(resposta_erro_aleatoria)
    ```
<br/>

#### **Aprendizados Efetivos**

Como esse foi o primeiro projeto que trabalhei, não somente na Fatec, mas com programação de fato, tive que
estudar bastante, aprendi como funciona uma linguagem interpretada e compilada, como iniciar um projeto do
zero, como tratar dados vindos da web e utilizar no sistema de acordo com a requisição feita pelo usuário,
além de definir escopo de funções.
</details></h4>

<h4><details>
<summary>Projeto 2: 2º Semestre de 2021</summary>

### **Parceiro Acadêmico**
Necto Systems

### **Objetivo do Projeto**

Desenvolvido para uma aplicação de coleta de informações do servidor para geração de série histórica. Nossa missão é desenvolver uma aplicação para coletar métricas periodicamente de um ou mais Sistemas Gerenciadores de **Banco de Dados** remoto. Através desta ferramenta o usuário terá informações para tomar decisões quanto a necessidade de manutenções, balanceamento e aumento de capacidade e melhoria no seus SGBDs, databases e na sua infra (Servidores).

Requisitos Funcionais:

  - Registros periódicos de métricas (diariamente / hora);
  - Disponibilidade de dados coletados em tempo real;
  - Histórico de métricas;
  - Relatórios com as métricas e valores limites atingidos durante a operação;
  - Cadastros de dados de conexão dos SGBDs (acesso a estatísticas por tabela).

Requisitos Não Funcionais:
  - Linguagem Java;
  - **Banco de Dados** Relacional.

### **Tecnologias adotadas na solução**

### **Banco de Dados**: Postgress
Como pedido pelo cliente, utilizamos o Postgress e todo o software for desenhado de acordo com os mecanismos
do Postgress.

### **Back-end**: Java
Para relização da API utilizamos a linguagem Java, com algumas bibliotecas, são elas:
  - java.sql (Para fazer operações no **Banco de Dados**);
  - java.io (Para manipular entrada e saída de arquivos);
  - java.util (Para utilizar toda a estrutura de dados fornecida pelo Java);
  - java.text (Para formatar entrada e saída de dados)

### **Ferramentas**: Intellij, Eclipse, Visual Studio Code, GitHub e Figma

### **Contribuições pessoais**

- Tratamento de erros:

    <details>

    ```java
    public class SQLRunTimeException extends RuntimeException {

        private static final long serialVersionUID = 1L;

        public SQLRunTimeException() {

        }

        public SQLRunTimeException(String message) {
            super(message);

        }

        public SQLRunTimeException(Throwable cause) {
            super(cause);

        }

        public SQLRunTimeException(String message, Throwable cause) {
            super(message, cause);

        }

        public SQLRunTimeException(String message, Throwable cause, boolean enableSuppression, boolean writableStackTrace) {
            super(message, cause, enableSuppression, writableStackTrace);

        }
    }
    ```
    </details>
    Em algumas operações que faziamos, era comum os erros voltarem de maneira não estruturada, para facilitar a leitura foi criado então essa forma de tratamento de exeception para que o erro fosse mais fácil de se ler.
- Leitura de dados passados pelo usuário:

    <details>

    ```java
    public class Leitor implements AutoCloseable {

        public Scanner scanner;

        public Leitor() {
            scanner = new Scanner(System.in);
        }

        public int getValor() {
            scanner.reset();
            int op = Integer.valueOf(scanner.nextLine());
            return op;
        }

        public String getTexto() {
            scanner.reset();
            String t = scanner.nextLine();
            return t;
        }

        @Override
        protected void finalize() throws Throwable {
            close();
        }

        @Override
        public void close() throws Exception {
            scanner.close();
        }
    }
    ```
    </details>
    Em outra classe do sistema temos um menu, e para utilizar era necessário leitura do teclado, para isso foi definido o Leito, com alguns métodos para garantir a eficácia, e que poderíamos utilizar de maneira bem estruturada.

- Métrica de tamanho de **Banco de Dados**:

    <details>

    ```java
    @SuppressWarnings("unused")
	public void tamanhoBancos() {
		ObterMetricas obterMetricas3 = new ObterMetricas(loginModel);
		List<TamanhoBancos> tamanhoBancos1 = obterMetricas3.TamanhoBanco();

		for (TamanhoBancos tamanhoBancos : tamanhoBancos1) {
			String nome = tamanhoBancos.getNome();
			String size = tamanhoBancos.getTamanho();
			String date = tamanhoBancos.getData();
		}
	}
    ```
    </details>

    Por fim, também foi feito a implementação de alguns métodos responsáveis por coletar métricas, nesse caso, de como obter o tamanho de **Banco de Dados**.

    <details>

    ```java
    public ArrayList<TamanhoBancos> TamanhoBanco() {

		String sql = "SELECT pg_database.datname, pg_size_pretty(pg_database_size(pg_database.datname)),current_timestamp(0) AS data FROM pg_database;";

		try {
			iniciarConexao();
			PreparedStatement pesquisa = con.prepareStatement(sql);
			ResultSet result = pesquisa.executeQuery();
			ArrayList<TamanhoBancos> lista = new ArrayList<TamanhoBancos>();

			String query = "INSERT INTO TamanhoBanco (datname,pg_size_pretty,data)VALUES (?, ?, ?)";
			PreparedStatement st = in.prepareStatement(query);

			while (result.next()) {
				TamanhoBancos tamTab = new TamanhoBancos();

				tamTab.setNome(result.getString("datname"));
				tamTab.setTamanho(result.getString("pg_size_pretty"));
				tamTab.setData(result.getString("data"));
				lista.add(tamTab);

				st.setString(1, tamTab.getNome());
				st.setString(2, tamTab.getTamanho());
				st.setString(3, tamTab.getData());
				st.executeUpdate();
			}
			return lista;
		} catch (SQLException e) {
			throw new SQLRunTimeException(e.getMessage(), e);
		} finally {
			desconecta();
		}
	}
    ```
    </details>

    Aqui temos basicamente um fluxo onde conecta a aplicação no **Banco de Dados** e para cada Banco dentro do SGBD realiza a operação de coletar e armazenar as informações, posterior a isso, é retornado a lista e desconecta do **Banco de Dados**.

#### **Aprendizados Efetivos**

Como esse foi o primeiro projeto que trabalhei com Java, não somente na Fatec, mas com programação de fato, tive que
estudar bastante, aprendi como funciona o Java, como realizar a conexão com um **Banco de Dados**, como tratar dados vindos do SGBD e utilizar no sistema de acordo com a requisição feita pelo usuário, além de definir escopo de funções.

</details></h4>

<h4><details>
<summary>Projeto 3: 1º Semestre de 2022</summary>

### **Parceiro Acadêmico**
MidAll

### **Objetivo do Projeto**

A empresa MidAll situada no Parque Tecnológico de São José dos Campos, propôs o seguinte desafio baseado na metodologia ágil Scrum. "Temos um problema para criação de promoções em um Ecommerce. Precisamos de uma solução inteligente onde, as mecânicas das promoções sejam feitas de forma flexível e de rápida atualização no sistema".

### **Tecnologias adotadas na solução**

### **Banco de Dados**: Microsoft SQL Server
Como requisitado pela Fatec, utilizamos um **Banco de Dados** relacional para armazenar o conteúdo das tabelas, como a escolha do BD era opcional optamos por utilizar
o Microsoft SQL Server

### **Back-end**: Java e Spring Boot
Para relização da API utilizamos a linguagem Java (Outro requisito Fatec) e o framework rest Spring Boot 

### **Front-end**: Angular, CSS, Bootstrap
Para construção da nos interface utilizamos o Angular, por alguns motivos, ele é um framework typescript, que é uma linguagem de progamação semelhante o Java e ao mesmo tempo tendo as caracteríticas do javascript, também utilizamos o Angular pois uma das dores do cliente era atualização simultânea de dados, o que podemos fazer facilmente com Angular utilizando o recurso two-way data binding.

### **Ferramentas**: IntelliJ IDEA, Visual Studio Code, GitHub e Figma

### **Contribuições pessoais**

- Exposição do endpoints das tabelas e camada de serviço;

    <details>

    ```java
    @RestController
    @RequestMapping(value = "/categories")
    public class CategoryResource {

        @Autowired
        private CategoryService categoryService;

        @Autowired
        private ModelMapper mapper;

        @GetMapping("/{id}")
        public ResponseEntity<?> find(@PathVariable Integer id) {
            Category cat = categoryService.find(id);
            return ResponseEntity.ok().body(cat);
        }

        @PostMapping
        public ResponseEntity<?> insert(@RequestBody Category obj) {
            obj = categoryService.insert(obj);
            URI uri = ServletUriComponentsBuilder.fromCurrentRequest().path("/{id}").buildAndExpand(obj.getId()).toUri();
            return ResponseEntity.created(uri).build();
        }

        @PutMapping("/{id}")
        public ResponseEntity<?> update(@RequestBody Category obj, @PathVariable Integer id) {

            obj.setId(id);
            obj = categoryService.update(obj);
            return ResponseEntity.noContent().build();
        }

        @DeleteMapping("/{id}")
        public ResponseEntity<?> delete(@PathVariable Integer id) {
            categoryService.delete(id);
            return ResponseEntity.noContent().build();

        }

        @GetMapping
        public ResponseEntity<List<CategoryDTO>> findAll() {
            List<Category> list = categoryService.findAll();

            List<CategoryDTO> listDto = list.stream().map(categoryService -> mapper.map(categoryService, CategoryDTO.class))
                    .collect(Collectors.toList());

            return ResponseEntity.ok().body(listDto);


        }

    }
    ```
    </details>

    Fui responsável por realizar a exposição de alguns endpoins baseado no modelo básico de dados. Como podemos ver, definindo a classe como um RestController e mapeando ela para uma URL desejada estaremos expondo aquele ponto de acesso quando iniciamos o TomCat, realizamos a exposição da entidade para que seja acessada via a uma URL na web, com o domínio que quisermos. Nesse caso, tudo que é relacionado a entidade Category terá seu ponto de acesso nesse endpoint que definimos, por ele realizamos as operações que desejamos e as devidas manipulações utilizando os métodos HTTPs para que sejam feitas operações no BD, na tabela Category.

    <details>

    ```java
    @Service
    public class CategoryService {

        @Autowired
        private CategoryRepository rep;

        public Category find(Integer id) {
            Optional<Category> cat = rep.findById(id);
            return cat.orElseThrow(() -> new ObjectNotFoundException(
                    "Object not found!: Id: " + id + ", Type: " + Category.class.getName()
            ));
        }

        public Category insert(Category obj){
            obj.setId(null);

            if(obj.getName().isEmpty()){
                throw new BadRequestException("Category with empty name");
            }

            for(Category cat : rep.findAll()){
                if(cat.getName().equals(obj.getName()) ){
                    throw new BadRequestException("Category does exist");
                }
            }
            return rep.save(obj);
        }

        public Category update(Category obj){
            find(obj.getId());
            if(obj.getName().equals(findAll())){
                throw new BadRequestException("Name similar to the one already registered");
            }
            return rep.save(obj);
        }

        public void delete(Integer id){
            find(id);
            if(find(id) == null){
                throw new BadRequestException("No ID entered");
            }
            rep.deleteById(id);
        }

        public List<Category> findAll() {
            List<Category> categoryList = rep.findAll();
            if (categoryList.isEmpty()) { //Nenhuma categoria cadastrada
                throw new BadRequestException("No category registered");
            }
            return rep.findAll();
        }
    }
    ```
    </details>

    Aqui temos um exemplo de um dos services que trabalhei, a camada de serviço é reponsável pelas regras de negócio da aplicação, ou seja, o que define o que a aplicação faz, o comportamento dela, aqui temos métodos de pesquisa, de inserção, de deleção, update, totalmente personalizados para a entidade em questão no caso a entidade "Category". É importante separar os Controllers dos Services não só por questão de organização, mas para garantir eficiência também, validações e regrar de negócio não são feitas nos controllers, para isso que defimos serviços.
<br/>

- Modelo básico de dados;

    Como fui responsável pelo template inicial do projeto, produzi o modelo básico de dados, que seria as classes que representam entidades:

    <details>

    ```java
    @Entity
    @Data
    @EqualsAndHashCode(of={"id"})
    @NoArgsConstructor
    public class Product implements Serializable {
        private static final long serialVersionUID = 1L;

        @Id
        @GeneratedValue(strategy= GenerationType.IDENTITY)
        private Integer id;

        private Integer discount;
        private String name;

        private Double price;

        private String description;

        @JsonIgnore
        @ManyToMany
        @JoinTable(
            name = "PRODUCT_CATEGORY",
            joinColumns = @JoinColumn(name = "product_id"),
            inverseJoinColumns = @JoinColumn(name = "category_id")
        )
        private List<Category> categories = new ArrayList<>();

        @ManyToMany(mappedBy = "product")
        private List<ProductPromotion> productPromotions = new ArrayList<>();

        public Product(Integer id, Integer discount, String name, Double price, String description) {
            this.id = id;
            this.discount = discount;
            this.name = name;
            this.price = price;
            this.description = description;
        }


    }
    ```
    </details>

    Como vemos acima, esse é um exemplo de como é feito uma entidade utilizando o spring-boot, elas necessitam da anotação @Entity para serem compreendidas como classes que são representações de entidades/tabelas, temos também outras anotações que são colocadas nos atributos para defini-los, cada atributo da classe é uma coluna da tabela.


- Módulo de configurações da aplicação;
    Também foi necessário que tivessemos um módulo responsável por realizar configurações antes da inicialização do TomCat, fiquei responsável por isso e desenvolvi algumas funções que tinham características específicas, como pro exemplo um configuration que definisse a nossa WebConfig, quais URLs poderiam estar acessando nosso Back-end, quais métodos seriam permitidos e assim por diante, com o intuito de não ter que repetir código em todos os endpoints que fossem implementados.

    <details>

    ```java
    @Configuration
    public class WebConfig {

        @Bean
        public FilterRegistrationBean<CorsFilter> corsFilterFilterRegistrationBean(){
            List<String> all = Arrays.asList("*");
            List<String> teste = Arrays.asList("http://localhost:4200/");

            CorsConfiguration corsConfiguration = new CorsConfiguration();
            corsConfiguration.setAllowedOrigins(teste);
            corsConfiguration.setAllowedHeaders(all);
            corsConfiguration.setAllowedMethods(all);
            corsConfiguration.setAllowCredentials(true);

            UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();

            source.registerCorsConfiguration("/**", corsConfiguration);

            CorsFilter corsFilter = new CorsFilter(source);

            FilterRegistrationBean<CorsFilter> filter = new FilterRegistrationBean<>(corsFilter);

            filter.setOrder(Ordered.HIGHEST_PRECEDENCE);

            return filter;
        }

    }
    ```
    </details>

    Essa classe acima, por exemplo, define algumas configurações web para o módulo CORS, aqui estamos basicamente
    definindo quais urls poderam realizar requisições para o Back-end.


- Integração do **Front-end** e **Back-end** utilizando Typescript;

    <details>

    ```typescript
    @Injectable({
    providedIn: 'root'
    })
    export class ProductsService {

    constructor(private http : HttpClient) { }

    insert( product : Product) : Observable<Product>{
        let obj = {
        "discount" : product.discount,
        "name" : product.name,
        "price" : product.price,
        "description" : product.description,
        "categories" : [
            {
                "id": product.categories
            }
        ]

        }
        return this.http.post<Product>('http://localhost:8080/products', obj)

    }


    getProducts() : Observable<any[]> {
        return this.http.get<Product[]>('http://localhost:8080/products')

    }

    getProductById(id : number) : Observable<Product>{
        return this.http.get<any>(`http://localhost:8080/products/${id}`)
    }

    update(id : number, product : Product) : Observable<Product> {
        let obj = {
        "name": product.name,
        "price": product.price,
        "categories": [
            {
                "id": product.categories
            }
        ]

        }
        return this.http.patch<Product>(`http://localhost:8080/products/${id}`, obj)
    }

    delete(product : Product) : Observable<any>{
        return this.http.delete<any>(`http://localhost:8080/products/${product.id}`)
    }
    }
    ```
    </details>

    Fiz também parte da integração do serviço em Angular com o Back-end, através do uso dos services do angular, onde eram criados métodos que enviavam objetos para as URLs definidas no Back-end de acordo com as regras pre-definidas utilizando o módulo HTTP do Angular.


- Desenvolvimento de algumas telas responsivas.

    <details>

    ```html
    <div class="container">
        <form #productForm="ngForm" (ngSubmit)="onSubmit()">

            <div class="row">
                <div class="col-md-12">
                    <div class="alert alert-success" role="alert" *ngIf="success == true">
                        Product saved/updated successfully!
                    </div>

                    <div class="alert alert-danger" role="alert" *ngFor="let erro of errors">
                        {{ erro }}
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col-md-12">
                    <div class="form-group">
                        <label>ID:</label>
                        <input type="text" class="form-control" disabled="true" [(ngModel)]="product.id" name="id">
                    </div>
                </div>
            </div>
            
            <div class="row">
                
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Name:</label>
                        <input type="text" class="form-control" [(ngModel)]="product.name" name="name">
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="form-group">
                        <label>Price:</label>
                        <input type="text" class="form-control" [(ngModel)]="product.price" name="price">
                    </div>
                </div>
                
            </div>

            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Description:</label>
                        <input type="text" class="form-control" [(ngModel)]="product.description" name="description">
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="form-group">
                        <label>Category:</label>
                        <input type="text" class="form-control" [(ngModel)]="product.categories" name="categories">
                    </div>
                </div>
                
            </div>

            <div class="row">
                <div class="col-md-4">
                    <button type="submit" class="btn btn-success" *ngIf="!product.id" >
                        <i class="fa fa-save"></i>
                        Save Product
                    </button>

                    <button type="submit" class="btn btn-primary" *ngIf="product.id" >
                        <i class="fa fa-sync-alt"></i>
                        Update Product
                    </button>

                    <button type="submit" class="btn btn-danger ml-2" routerLink="/products-list">
                        <i class="fa fa-arrow-alt-circle-left"></i>
                        return
                    </button>
                </div>

            </div>
        
        </form>
    </div>
    ```
    </details>

    Por fim, participei também da criação de algumas telas utilizando HTML, Bootstrap e Angular, realizando as análises e implementando recursos do Angular de acordo com a necessidade de cada tela e de cada endpoint ao qual o Front-end iria consumir.


#### **Aprendizados Efetivos**

Durante esse projeto eu ainda não tinha muita noção de como funcionava a o conjunto do Back-end e Front-end, como que se utilizava os protocolos de comunicação entre serviços feitos em diferentes linguagens e nem quais configurações havia de ser feito tanto no back quanto no front para garantir que essa comunicação acontessesse de maneira controlada e esperada, portanto entendo que os meus **Aprendizados Efetivos** foram como integrar microservices, como relizar modularizar configurações que devem subir na inicialização do TomCat e como estabelecer protocolos de comunicação e expor a aplicação como um todo de maneira adequada para a web.

</details></h4>

<h4><details>
<summary>Projeto 4: 2º Semestre de 2022</summary>

### **Parceiro Acadêmico**
Subter

### **Objetivo do Projeto**

Temos um desafio de sincronização dos dados administrativos, financeiros e operacionais referentes aos serviços prestados pela empresa. A falta de organização dos dados acarreta lentidão para atender chamados, e confusão na interpretação dos indicadores comerciais e financeiros.

- Requisitos Funcionais

  - Cadastros de Usuários, Equipamentos e Horários
  - Usuários devem ter perfis diferentes (administrador, suporte, cliente)
  - Registro de chamados
  - Acompanhamento de chamados de ponta a ponta
  - **Front-end** para entrada e interpretação de dados.

- Requisitos Não Funcionais

    - Linguagem Java Web Server-Side (Requisito Exigido Fatec)
    - PL / SQL (Requisito Exigido Fatec)
    - GIT (Requisito Exigido Fatec)
    - Vue.js ou Flutter (Front-end).

### **Tecnologias adotadas na solução**

### **Banco de Dados**: Oracle Cloud
Como requisitado pela Fatec, utilizamos um **Banco de Dados** Oracle Cloud para armazenar o conteúdo das tabelas.

### **Back-end**: Java e Spring Boot
Para relização da API utilizamos a linguagem Java (Outro requisito Fatec) e o framework rest Spring Boot 

### **Front-end**: VueJs, CSS, Bootstrap
Para construção da nos interface utilizamos o VueJs, como requisitado pela fatec.

### **Ferramentas**: IntelliJ IDEA, Docker, Visual Studio Code, GitHub e Figma

### **Contribuições pessoais**
- Exposição do endpoints das tabelas e camada de serviço:

    <details>

    ```java
    @RestController
    @RequestMapping("/api/chamados")
    public class ChamadoController {

        @Autowired
        private ChamadoService chamadoService;

        @PreAuthorize("hasAnyRole('CLIENT', 'SUPORTE')")
        @GetMapping
        @JsonView(View.ChamadoView.class)
        public List<Chamado> getAllChamados(){

            return chamadoService.getAllChamados();
        }

        @PreAuthorize("hasAnyRole('CLIENT','SUPORTE')")
        @PostMapping
        @ResponseStatus(HttpStatus.CREATED)
        @JsonView(View.ChamadoView.class)
        public Chamado saveChamado(@RequestBody @Valid Chamado chamado){

            return chamadoService.save(chamado);  
        }

        @PreAuthorize("hasAnyRole('CLIENT', 'SUPORTE')")
        @GetMapping("/{id}")
        @JsonView(View.ChamadoView.class)
        public Chamado getChamadoById(@PathVariable Integer id){

            return chamadoService.getChamadoById(id);
        }
        
        @PreAuthorize("hasAnyRole('CLIENT', 'SUPORTE')")
        @PatchMapping("/{id}")
        @JsonView(View.ChamadoView.class)
        public Chamado updateChamadoById(@PathVariable Integer id, @RequestBody Chamado chamado){

            return chamadoService.updateChamadoById(id, chamado);
        }
        
        @PreAuthorize("hasAnyRole('CLIENT', 'SUPORTE')")
        @DeleteMapping("/{id}")
        @JsonView(View.ChamadoView.class)
        public void deleteChamadoById(@PathVariable Integer id){

            chamadoService.deleteChamadoById(id);
        }
        
    }
    ```
    </details>

    Fui responsável por realizar a exposição de alguns endpoins baseado no modelo básico de dados. Como podemos ver, definindo a classe como um RestController e mapeando ela para uma URL desejada estaremos expondo aquele ponto de acesso quando iniciamos o TomCat, realizamos a exposição da entidade para que seja acessada via a uma URL na web, com o domínio que quisermos. Nesse caso, tudo que é relacionado a entidade Chamado terá seu ponto de acesso nesse endpoint que definimos, por ele realizamos as operações que desejamos e as devidas manipulações utilizando os métodos HTTPs para que sejam feitas operações no BD, na tabela Chamado.


- Modelo básico de dados:

    Como fui responsável pelo template inicial do projeto, produzi o modelo básico de dados, que seria as classes que representam entidades, utilizando como guia a modelagem feita por outro membro do time.

    <details>

    ```java
    @Entity(name = "CHAMADO")
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    @Builder
    public class Chamado implements Serializable{

        private static final long serialVersionUID = 1L;


        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        @Column(name = "numero_chamado")
        @JsonView({View.ChamadoView.class, View.UsuarioView.class, View.TipoServicoView.class})
        private Integer id;

        @JoinColumn(name="codigo_usuario")
        @ManyToOne(fetch = FetchType.LAZY)
        @JsonView({View.ChamadoView.class})
        private Usuario usuarioChamado;
        
        @JsonView({View.ChamadoView.class, View.UsuarioView.class})
        @ManyToOne()
        @JoinColumn(name = "tipo_servico_codigo")
        private TipoServico tipoChamado;

        @Column(name = "criticidade_chamado", nullable = false)
        @NotEmpty(message = "O Campo criticidade é obrigatório")
        @JsonView({View.ChamadoView.class, View.UsuarioView.class})
        private String criticidadeChamado;

        @Column(name = "data_chamado", nullable = false)
        @JsonFormat(pattern = "dd/MM/yyyy")
        @JsonView({View.ChamadoView.class})
        private LocalDate dataChamado;

        @Column(name = "assunto_chamado", nullable = false, length = 120)
        @NotEmpty(message = "O Campo assunto é obrigatório")
        @JsonView({View.ChamadoView.class, View.UsuarioView.class, View.TipoServicoView.class})
        private String assuntoChamado;

        @Column(name = "descricao_chamado", nullable = false, length = 300)
        @NotEmpty(message = "O Campo descrição é obrigatório")
        @JsonView({View.ChamadoView.class, View.UsuarioView.class})
        private String descricaoChamado;

        @Column(name = "situacao_chamado", nullable = false)
        @NotEmpty(message = "O Campo situação é obrigatório")
        @JsonView({View.ChamadoView.class})
        private String situacaoChamado;

        @Column(name = "solucao_chamado", nullable = false)
        @JsonView({View.ChamadoView.class})
        private String solucaoChamado;

        @Column(name = "encerramento_chamado")
        @JsonFormat(pattern = "dd/MM/yyyy")
        @JsonView({View.ChamadoView.class})
        private LocalDate encerramentoChamado;

        @JoinColumn(name="numero_agendamento")
        @OneToOne(mappedBy = "chamadoAgendamento", cascade = CascadeType.ALL)
        @JsonView({View.ChamadoView.class})
        private Agendamento agendamento;
        
        @PrePersist
        public void presPersist(){
            setDataChamado(LocalDate.now());
        }

    }
    ```
    </details>

    Como vemos acima, esse é um exemplo de como é feito uma entidade utilizando o spring-boot, elas necessitam da anotação @Entity para serem compreendidas como classes que são representações de entidades/tabelas, temos também outras anotações que são colocadas nos atributos para defini-los, cada atributo da classe é uma coluna da tabela.


- Módulo de configurações da aplicação:

    Também foi necessário que tivessemos um módulo responsável por realizar configurações antes da inicialização do TomCat, fiquei responsável por isso e desenvolvi algumas funções que tinham características específicas, como pro exemplo um configuration que definisse a nossa WebConfig, quais URLs poderiam estar acessando nosso Back-end, quais métodos seriam permitidos e assim por diante, com o intuito de não ter que repetir código em todos os endpoints que fossem implementados.

    <details>

    ```java
    @Configuration
    public class WebConfig {

        @Bean
        public FilterRegistrationBean<CorsFilter> corsFilterFilterRegistrationBean(){
            List<String> all = Arrays.asList("*");
            List<String> teste = Arrays.asList("http://localhost:4200/");

            CorsConfiguration corsConfiguration = new CorsConfiguration();
            corsConfiguration.setAllowedOrigins(teste);
            corsConfiguration.setAllowedHeaders(all);
            corsConfiguration.setAllowedMethods(all);
            corsConfiguration.setAllowCredentials(true);

            UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();

            source.registerCorsConfiguration("/**", corsConfiguration);

            CorsFilter corsFilter = new CorsFilter(source);

            FilterRegistrationBean<CorsFilter> filter = new FilterRegistrationBean<>(corsFilter);

            filter.setOrder(Ordered.HIGHEST_PRECEDENCE);

            return filter;
        }

    }
    ```
    </details>

    Essa classe acima, por exemplo, define algumas configurações web para o módulo CORS, aqui estamos basicamente
    definindo quais urls poderam realizar requisições para o Back-end.


- Security:

    <details>

    ```java
    @Slf4j
    public class JWTAuthenticationFilter extends UsernamePasswordAuthenticationFilter {

        private final AuthenticationManager authenticationManager;

        public JWTAuthenticationFilter(AuthenticationManager authenticationManager){
            this.authenticationManager = authenticationManager;
        }

        @Override
        public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException {
            String email = request.getParameter("email");
            String password = request.getParameter("password");
            log.info("Username is {} and password is {}", email, password);
            UsernamePasswordAuthenticationToken authenticationToken = new UsernamePasswordAuthenticationToken(email, password);
            log.info("Token {}", authenticationToken);
            return authenticationManager.authenticate(authenticationToken);
        }

        @Override
        protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authentication) throws IOException, ServletException {
            UserDetails user =  (UserDetails)authentication.getPrincipal();
            Algorithm algorithm = Algorithm.HMAC256("secret".getBytes());
            String access_token = JWT.create()
                    .withSubject(user.getUsername())
                    .withExpiresAt(new Date(System.currentTimeMillis() + 60 * 60 * 1000))
                    .withIssuer(request.getRequestURL().toString())
                    .withClaim("roles", user.getAuthorities().stream().map(GrantedAuthority::getAuthority).collect(Collectors.toList()))
                    .sign(algorithm);
            String refresh_token = JWT.create()
                    .withSubject(user.getUsername())
                    .withExpiresAt(new Date(System.currentTimeMillis() + 60 * 60 * 1000))
                    .withIssuer(request.getRequestURL().toString())
                    .sign(algorithm);

            Map<String, String> tokens = new HashMap<>();
            tokens.put("access_token", access_token);
            tokens.put("refresh_token", refresh_token);
            tokens.put("autorizacao", user.getAuthorities().iterator().next().getAuthority());
            response.setContentType(APPLICATION_JSON_VALUE);
            new ObjectMapper().writeValue(response.getOutputStream(), tokens);

        }
    }
    ```
    </details>

    Esse código implementa um filtro de autenticação JWT em uma aplicação web.

    A classe **JWTAuthenticationFilter** é uma subclasse de **UsernamePasswordAuthenticationFilter**, que é usada para autenticar usuários usando seus nomes de usuário e senhas. No método **attemptAuthentication()**, a classe extrai os dados de nome de usuário e senha da requisição HTTP e cria um token de autenticação do tipo **UsernamePasswordAuthenticationToken**. O token de autenticação é então enviado para o **AuthenticationManager**, que valida as credenciais do usuário.

    Se as credenciais do usuário forem validadas com sucesso, o método **successfulAuthentication()** é chamado. Nesse método, um token JWT é criado usando a biblioteca java-jwt. O token contém o nome de usuário, uma data de expiração, um emissor e as permissões do usuário (também chamadas de funções). O token é então adicionado ao objeto Map e enviado como uma resposta HTTP com um status de 200.

    <details>

    ```java
    public class JWTAuthorizationFilter extends OncePerRequestFilter {

        private final ObjectMapper objectMapper = new ObjectMapper();
        private final JWTVerifier verifier = JWT.require(Algorithm.HMAC256("secret".getBytes())).build();
        private final List<String> ignoredPaths = List.of("/auth/login", "/auth/token/refresh");

        protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
            if (ignoredPaths.contains(request.getServletPath())) {
                filterChain.doFilter(request, response);
                return;
            }

            String authorizationHeader = request.getHeader(AUTHORIZATION);
            if (authorizationHeader != null && authorizationHeader.startsWith("Bearer ")) {
                try {
                    String token = authorizationHeader.substring("Bearer ".length());
                    DecodedJWT decodedJWT = verifier.verify(token);
                    String username = decodedJWT.getSubject();
                    String[] roles = decodedJWT.getClaim("roles").asArray(String.class);
                    Collection<SimpleGrantedAuthority> authorities = new ArrayList<>();
                    Arrays.stream(roles).forEach(role -> {
                        authorities.add(new SimpleGrantedAuthority(role));
                    });
                    UsernamePasswordAuthenticationToken authenticationToken = new UsernamePasswordAuthenticationToken(username, null, authorities);
                    SecurityContextHolder.getContext().setAuthentication(authenticationToken);
                    filterChain.doFilter(request, response);
                } catch (JWTVerificationException e) {
                    response.setHeader("error", e.getMessage());
                    response.setStatus(HttpServletResponse.SC_FORBIDDEN);
                    Map<String, String> error = Map.of("error_message", e.getMessage());
                    response.setContentType(MediaType.APPLICATION_JSON_VALUE);
                    try (OutputStream out = response.getOutputStream()) {
                        objectMapper.writeValue(out, error);
                    }
                }
            } else {filterChain.do}
        }
    }
    ```
    </details>

    Esse código é uma implementação de um filtro de autorização baseado em JWT (JSON Web Token). A classe **JWTAuthorizationFilter** extende a classe OncePerRequestFilter, que é um filtro do Spring que garante que o filtro seja executado apenas uma vez por solicitação.

    A classe tem uma lista de caminhos ignorados, que são as rotas que não precisam ser autenticadas. Quando uma solicitação é feita para um desses caminhos, o filtro é ignorado e o controle é passado para o próximo filtro da cadeia.

    Para as solicitações que não estão na lista de caminhos ignorados, o filtro verifica se a solicitação contém um token JWT válido no cabeçalho de autorização. Se não houver nenhum token JWT no cabeçalho de autorização, a solicitação é passada para o próximo filtro da cadeia. Se houver um token JWT válido, o filtro extrai o nome de usuário e as permissões do token e cria um objeto **UsernamePasswordAuthenticationToken** contendo essas informações. Em seguida, o filtro armazena esse objeto de autenticação no contexto de segurança e passa a solicitação para o próximo filtro da cadeia.

    Se o token JWT for inválido, o filtro retorna um erro 403 Forbidden com uma mensagem de erro JSON no corpo da resposta.

    <details>

    ```java
    @Configuration
    @EnableWebSecurity
    @RequiredArgsConstructor
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class SecurityConfig extends WebSecurityConfigurerAdapter {

        private static final String[] PUBLIC_MATCHERS = {
        //"/h2-console/**"
        };

        private static final String[] PUBLIC_MATCHERS_GET = {

        };

        private static final String[] PUBLIC_MATCHERS_POST = {
                "/api/usuarios/**",
                "/auth/login/**",
        };

        private final UserDetailsService userDetailsService;
        private final BCryptPasswordEncoder bCryptPasswordEncoder;

        @Override
        protected void configure(HttpSecurity http) throws Exception {

            JWTAuthenticationFilter jWTAuthenticationFilter = new JWTAuthenticationFilter(authenticationManagerBean());
            jWTAuthenticationFilter.setFilterProcessesUrl("/auth/login");

            http.csrf().disable();
            http.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);

            http.authorizeRequests()
                    .antMatchers(PUBLIC_MATCHERS)
                    .permitAll()
                    .antMatchers(HttpMethod.GET, PUBLIC_MATCHERS_GET)
                    .permitAll()
                    .antMatchers(HttpMethod.POST, PUBLIC_MATCHERS_POST)
                    .permitAll()
                    .anyRequest()
                    .authenticated();

            http.addFilter(jWTAuthenticationFilter);
            http.addFilterBefore(new JWTAuthorizationFilter(), UsernamePasswordAuthenticationFilter.class);
        }

        @Override
        protected void configure(AuthenticationManagerBuilder auth) throws Exception {
            auth.userDetailsService(userDetailsService).passwordEncoder(bCryptPasswordEncoder);
        }

        @Bean
        public BCryptPasswordEncoder bCryptPasswordEncoder() {
            return new BCryptPasswordEncoder();
        }

        @Bean
        @Override
        public AuthenticationManager authenticationManagerBean() throws Exception {
            return super.authenticationManagerBean();
        }

        @Override
        public void configure(WebSecurity web) throws Exception {
            web.ignoring()
                    .antMatchers("/h2-console/**")
                    .antMatchers(HttpMethod.POST, "/api/usuarios/auth/signup/suporte")
                    .antMatchers(HttpMethod.POST, "/api/usuarios/auth/signup/client")
                    .antMatchers(HttpMethod.GET, "/api/usuarios/auth/token/refresh");
        }

    ```
    </details>

    Esse código implementa a configuração de segurança em uma aplicação Spring Boot. A classe extende a classe WebSecurityConfigurerAdapter, que permite a configuração de regras de segurança da aplicação.

    O método **configure(HttpSecurity http)** configura as regras de segurança para a aplicação. Por exemplo, as URLs públicas são permitidas para os PUBLIC_MATCHERS, tanto para as solicitações GET quanto para as POST. Qualquer outra solicitação exige autenticação e autorização. O método também adiciona filtros para autenticação e autorização.

    O método **configure(AuthenticationManagerBuilder auth)** configura a autenticação baseada em **UserDetailsService** e **BCryptPasswordEncoder**.

    O método **configure(WebSecurity web)** configura a segurança para os recursos estáticos que não requerem autenticação. Por exemplo, a URL para o console H2 e alguns endpoints que lidam com o registro de usuários.

    Os beans de **BCryptPasswordEncoder** e **AuthenticationManager** são configurados e disponíveis para uso no contexto da aplicação.

    <details>

    ```java
    @Service @RequiredArgsConstructor @Transactional @Slf4j
    public class ApplicationUserDetails implements UserDetailsService {

        private final ApplicationUserRepository applicationUserRepository;

        @Override
        public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
            ApplicationUser applicationUser = applicationUserRepository.findByEmail(username);
            if(applicationUser == null){
                log.error("User not found in the database");
                throw new UsernameNotFoundException("User not found in the database");
            }else{
                log.info("User found in the database: {}", username);
            }
            log.info("Username {} and password {}", applicationUser.getEmail(), applicationUser.getPassword());
            return applicationUser;
        }
    }
    ```
    </details>

    Esse código define uma classe chamada **ApplicationUserDetails** que implementa a interface **UserDetailsService**. 

    A interface UserDetailsService é usada pelo Spring Security para carregar informações de usuário durante a autenticação. A implementação ApplicationUserDetails implementa o método loadUserByUsername, que recebe um nome de usuário como parâmetro e retorna um objeto UserDetails que representa as informações do usuário encontrado.

    O código usa uma instância do ApplicationUserRepository (injetado por meio do construtor) para procurar um ApplicationUser por e-mail (que é considerado o nome de usuário nesse caso). Se o usuário não for encontrado, uma exceção UsernameNotFoundException é lançada. Se o usuário for encontrado, um log é criado com informações de depuração e o objeto ApplicationUser é retornado como UserDetails.

    ```java
    @PreAuthorize("hasAnyRole('CLIENT', 'SUPORTE')")
    @DeleteMapping("/{id}")
    @JsonView(View.ChamadoView.class)
    public void deleteChamadoById(@PathVariable Integer id){

        chamadoService.deleteChamadoById(id);
    }
    ```

    Aqui temos um exemplo de como é interpretado as roles definidas no service nos endpoints, quando você realiza o login, acontece a autenticação e é verificado qual é a role daquele usuário, e a role e token são guardados na sessão, enquanto o usuário utiliza o sistema, tudo que é exposto em um endpoint é anotado com **@PreAuthorize("hasAnyRole('ROLE', 'ROLE', ...)")**, que define quais níveis de usuário podem realizar a operação requisitada.


- JsonView:

    Quando temos classes relacionadas, como por exemplo, Empresa e Serviço, é comum a necessidade de ser visualizado esses dados,
    tanto em uma tabela ou em outra. Porém o que acontece se quisermos visualizar dados da empresa e também os serviços atrelados
    àquela empresa? Se simplesmente utilizarmos uma operação de get, sem configurações iniciais, a requisição vai entrar em Loop
    por causa do relacionamento e retornar um erro. Então decidimos assim usar um componente de JsonIgnore em um dos atributos de 
    relacionamentos dessa classe para que não quebre, mas continuamos com o problema de não conseguir visualizar esses dados, e 
    para isso que utilizamos o JsonView.

    <details>

    ```java
    public class View {

        public static class ChamadoView {};

        public static class EmpresaView {};

        public static class EquipamentoView {};

        public static class EquipamentoSerieView {};

        public static class InstalacaoView {};

        public static class ServicoView {};

        public static class TipoServicoView {};

        public static class UsuarioView {};

        public static class AgendamentoView {};

    }
    ```
    </details>

    Essa classe é a referência pro JsonView, cada método representa a abstração que será usada como View para cada tabela que temos,
    e cada atributo da entidade, recebera uma anotação para o seu JsonView respectivo.

    <details>

    ```java
    @Entity(name = "USUARIO")
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    @Builder
    public class Usuario implements Serializable{

        private static final long serialVersionUID = 1L;

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        @Column(name = "codigo_usuario")
        @JsonView({View.UsuarioView.class, View.ChamadoView.class, View.EmpresaView.class})
        private Integer id;

        @JoinColumn(name="codigo_empresa")
        @ManyToOne()
        @JsonView({View.UsuarioView.class})
        private Empresa empresa;

    }
    ```
    </details>

    Nesse código vemos como é configurado o View, em cada atributo da classe é colocado a anotação
    **@JsonView**, que recebe uma chave, que primeiramente tem apenas o View da classe, note que
    o atributo do relacionamento com empresa também receve o **@JsonView**, então por que não temos
    um erro quando tentandos fazer o get? Porque estamos definindo atributos de maneira isolada,
    veja abaixo.

    ```java
    @JsonView({View.UsuarioView.class, View.ChamadoView.class, View.EmpresaView.class})
    private Integer id;
    ```

    Utilizando esse exemplo, veja que a primeira anotação de View é a da própria classe Usuario, e logo
    após é definido que outros Views de classes que se relacionam com Usuario podem realizar um get naquele
    atributo, e por isso, mesmo coletando todos os atributos em alguns casos, se a anotação não for colocada
    no relacionamento, não teremos problema para visualizar o que queremos.

- Dockerfile;
    Back-end|
    -------|
    ```Dockerfile
    FROM openjdk:11-jdk-slim
    ARG JAR_FILE=target/*.jar
    COPY ${JAR_FILE} app.jar
    RUN bash -c 'touch /app.jar'
    ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
    ```

    Front-end|
    -------|
    ```Dockerfile
    FROM node:lts-alpine
    RUN npm install -g http-server
    WORKDIR /app
    COPY package*.json ./
    RUN npm install
    COPY . .
    RUN npm run build
    EXPOSE 4200
    CMD [ "http-server", "dist" ]
    ```
    Por fim, defini o Dockerfile para ambos os serviços e através dele podemos gerar as images e utilizar como containers,
    dessa forma, não é necessário nada para rodar, além do docker engine.

#### **Aprendizados Efetivos**

Durante esse projeto eu ainda não tinha muita noção de como definir níveis de acesso e como adequar regras de security para ser utilizado em todo o sistema, garantindo uma aplicação com um nível adequado de security e safety. Também não tinha conhecimento de como otimizar a entrada de dados e filtrar utilizando JsonView e de como configurar as imagens para posteriomente serem utilizadas com um **Banco de Dados** em cloud. portanto entendo que os meus **Aprendizados Efetivos**foram baseados em definir níveis de acesso e configurar uma camada do serviços que cuida de autenticação e autorização, como definir filtros de dados e como construir a imagem e usar todo o serviço
com um **Banco de Dados** na cloud.
</details></h4>

<h4><details>
<summary>Projeto 5: 1º Semestre de 2023</summary>

### **Parceiro Acadêmico**
MidAll

### **Objetivo do Projeto**

Automatizar a jornada de download dos arquivos, armazenados em uma plataforma de vídeos, realizando essa transferência para cloud, através do desenvolvimento de uma aplicação como serviço, tendo como funcionalidade com o usuário somente um menu de configuração, que terão os parâmetros necessários para que o serviço de download processe automaticamente, gerando alertas caso ocorra erro no processamento. Salvar os metadados dos arquivos, para construção de um dashboard para acompanhamento da execução do serviço e posterior análise de resultados e indicadores (ex: quantidade de arquivos transferidos, quantidade de bytes transferidos, tempo de transferência e etc).

Requisitos Funcionais:

- Aplicação 1 - Construir uma aplicação que rodará servidor local para configuração e parametrização do serviço;

- Aplicação 1 - Nessa aplicação, criar tela para configuração do sistema (com todas as configurações que a aplicação atual já tem), incluindo também a limitação de consumo de banda de rede e tempo para verificação de novos arquivos para download;

- Aplicação 1 - Criar também, tela para configuração da conta de acesso a api (guardar de um jeito seguro);

- Aplicação 1 - Emitir alerta no S.O. avisando que novos arquivos foram baixados;

- Aplicação 1 - Criar tela de histórico de arquivos baixados;

- Aplicação 2 - Construir uma API que será o serviço que buscará os arquivos que devem ser enviados para Cloud;

- Aplicação 2 - Conectar com a api de arquivos (utilizar outro fornecedor, diferente do usado no requisito anterior. Pode ser Google Drive, AWS S3, Dropbox e etc.);

- Aplicação 2 - Realizar o download dos arquivos, seguindo as configurações realizadas na aplicação 1;

- Criar dashboard para acompanhamento das execuções (pode ser construído).

### **Tecnologias adotadas na solução**

### **Banco de Dados**: MySQL, SQLite
Como requisitado pelo, utilizamos um Banco de Dados relacional local para a aplicação que ficará do lado do cliente, como a escolha do BD era opcional optamos por utilizar o SQLite, e na segunda aplicação, utilizamos MySQL.

### **Back-end**: Python, Flask
Para relização da API utilizamos a linguagem Python, e para expor a aplicação utilizamos o framework Flask.

### **Front-end**: VueJS, CSS, Bootstrap
Para construção da nos interface utilizamos o VueJS.

### **Ferramentas**: Visual Studio Code, GitHub e Figma

### **Contribuições pessoais**

</details></h4>
