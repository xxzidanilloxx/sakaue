<div align="center">
  <h1>Testes Unitários</h1>
</div>

## 📖 Definição

Segundo Martin Fowler, testes unitários são uma prática que visa testar o método do código para verificar sua funcionalidade correta. Ele destaca as abordagens "solitária" e "sociável": a primeira simula dependências com mocks, enquanto a segunda permite interações entre componentes reais.

![abordagens-testes-unitarios](https://github.com/xxzidanilloxx/sakaue/blob/main/assets/abordagens-testes-unitarios.svg)

É recomendado que os testes sejam rápidos e executados frequentemente para facilitar a detecção de erros logo após mudanças, promovendo assim qualidade e estabilidade no desenvolvimento contínuo.

## ⚙️ Testes unitários no contexto do processo de desenvolvimento

A seguir está o fluxograma dos testes unitários no contexto do processo de desenvolvimento:

![fluxograma-testes-unitarios](https://github.com/xxzidanilloxx/sakaue/blob/main/assets/fluxograma-testes-unitarios.svg)

> [!IMPORTANT]
> No processo de desenvolvimento, os testes unitários são executados automaticamente quando ocorre um trigger, que, neste caso, é a abertura de um pull request para a branch develop.

## 📘 Orientações para implementação de testes unitários

> [!IMPORTANT]
> Recomendações gerais: Ao incluir um novo teste e perceber que um teste já existente interfere em sua execução, é necessária refatoração imediata. A responsabilidade pela correção deve ser da pessoa que identificou o problema, garantindo eficiência e promovendo a colaboração na equipe.

### 🖥️ Back-end:

A seguir está a estrutura e as orientações para a organização e implementação de testes unitários no back-end do projeto:

#### 📂 Estrutura
<details open>
<summary>
  <b> Exemplo de Estrutura </b>
</summary>

```plaintext
api-back/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── br.gov.sp.cps.api.pixel/
│   │   │       ├── core/
│   │   │       │   ├── service/
│   │   │       │   │   └── exemplo/
│   │   │       │   │      └── ExemploService.java
│   │   │       │   └── usecase/
│   │   │       │       └── exemplo/
│   │   │       │          └── ExemploUseCase.java
│   │   │       ├── inbound.rest/
│   │   │       ├── outbound/
│   │   │       └── PixelApplication
│   │   └── resources/
│   └── test/
│       ├── java/
│       │   └── br.gov.sp.cps.api.pixel/
│       │       ├── core/
│       │       │   ├── service/
│       │       │   │   └── exemplo/
│       │       │   │      └── ExemploServiceTest.java
│       │       │   └── usecase/
│       │       │       └── exemplo/
│       │       │          └── ExemploUseCaseTest.java
│       │       ├── inbound.rest/
│       │       ├── outbound/
│       │       └── ApplicationTests.java
│       └── resources/
├── pom.xml
└── README.md
```
</details>

#### 📋 Orientações

1️⃣ Nome dos arquivos de teste:
   - Deve ser utilizado o mesmo nome da classe testada, adicionando o sufixo `Test`.  
     Exemplo:  
     - Classe: `ExemploService.java`  
     - Teste: `ExemploServiceTest.java`  

2️⃣ Localização dos testes: 
   - Os testes devem ser colocados no diretório correspondente em `src/test/java`, espelhando a estrutura de `src/main/java`.
     Exemplo:
     - Serviços: `src/test/java/br.gov.sp.cps.api.pixel/core/service/`.  
     - Casos de Uso: `src/test/java/br.gov.sp.cps.api.pixel/core/usecase/`.

### 🌐 Front-end:

A seguir está a estrutura e as orientações para a organização e implementação de testes unitários no front-end do projeto:

#### 📂 Estrutura
<details open>
<summary>
    <b>Exemplo de Estrutura</b>
</summary>

```plaintext
api/
├── src/
│   ├── app/
│   │   ├── components/
│   │   │   └── exemplo/
│   │   │       ├── exemplo.component.ts
│   │   │       └── exemplo.component.spec.ts
│   │   └── app.module.ts
│   ├── assets/
│   ├── environments/
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   └── test.ts
├── angular.json
├── package.json
├── tsconfig.json
└── README.md
```
</details>

#### 📋 Orientações

1️⃣ Nome dos arquivos de teste:
   - Deve ser utilizado o mesmo nome do arquivo testado, adicionando o sufixo `.spec.ts`.  
     Exemplo:  
     - Componente: `exemplo.component.ts`  
     - Teste: `exemplo.component.spec.ts`.

2️⃣ Localização dos testes: 
   - Os testes devem ser colocados no mesmo diretório do componente ou serviço correspondente.

## 💡 Exemplos práticos

A seguir estão exemplos de testes unitários implementados no [Projeto Integrador](https://github.com/api-5-sem/api-documentation) que está sendo desenvolvido neste semestre:

### 🧪 Testes unitários no back-end

<details open>
<summary>
  <b> PermissaoUCTest.java </b>
</summary>

```java
@SpringBootTest(classes = PixelApplication.class)
@ActiveProfiles("test")
class PermissaoUCTest {

    @Autowired
    private PermissaoRepository permissaoRepository;

    @Autowired
    private PermissaoUC permissaoUC;

    @BeforeEach void setUp() {
        Permissao permissao = new Permissao(1, "TESTE", "Teste", null);
        permissaoRepository.salvar(permissao);
    }

    @Test
    void deveListarTodasAsPermissoes() {
        List<Permissao> resultado = permissaoUC.listar();

        assertEquals(1, resultado.size());
        assertEquals("TESTE", resultado.get(0).getChave());
    }
}
```
</details>

<details open>
<summary>
  <b> GrupoUCTest.java </b>
</summary>

```java
@SpringBootTest(classes = PixelApplication.class)
@ActiveProfiles("test")
class GrupoUCTest {

    @Autowired
    private GrupoRepository grupoRepository;

    @Autowired
    private GrupoUC grupoUC;

    @BeforeEach
    void setUp(){
        Grupo grupo = new Grupo(1L, "TESTE", null);
        grupoRepository.salvar(grupo);
    }

    @Test
    void deveListarTodosOsGrupos() {
        List<Grupo> resultado = grupoUC.listar();

        assertEquals(1, resultado.size());
        assertEquals("TESTE", resultado.get(0).getNome());
    }
}
```
</details>

### 🧪 Testes unitários no front-end

<details open>
<summary>
  <b> table-list.component.spec.ts </b>
</summary>

```typescript
describe('TableListComponent', () => {
  let component: TableListComponent;
  let fixture: ComponentFixture<TableListComponent>;

  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ TableListComponent ]
    })
    .compileComponents();
  }));

  beforeEach(() => {
    fixture = TestBed.createComponent(TableListComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```
</details>

<details open>
<summary>
  <b> typography.component.spec.ts </b>
</summary>

```typescript
describe('TypographyComponent', () => {
  let component: TypographyComponent;
  let fixture: ComponentFixture<TypographyComponent>;

  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ TypographyComponent ]
    })
    .compileComponents();
  }));

  beforeEach(() => {
    fixture = TestBed.createComponent(TypographyComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```
</details>

## 🛠️ Tecnologias utilizadas

### 🖥️ Back-end:

<div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/java.svg" alt="java" width="50" height="50">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/spring.svg" alt="spring" width="50" height="50">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/junit.svg" alt="junit" width="50" height="50">
</div>

### 🌐 Front-end:

<div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/typescript.svg" alt="typescript" width="50" height="50">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/angular.svg" alt="angular" width="50" height="50">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/jasmine.svg" alt="jasmine" width="50" height="50">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/karma.svg" alt="karma" width="50" height="50">
</div>

## 🎯 Conclusão

A prática de testes unitários proporciona uma descoberta eficiente de bugs, permitindo detectar erros de entrada, saída ou lógica em blocos de código antes que eles alcancem o ambiente de produção. Com o mesmo conjunto de testes sendo executado continuamente após alterações no código, é possível identificar falhas relacionadas a bugs de maneira ágil.

Além disso, os testes unitários aceleram a identificação de problemas, reduzindo o tempo gasto com depuração. Eles ajudam os desenvolvedores a localizar rapidamente a parte exata do código que apresenta o erro, promovendo um ciclo de desenvolvimento mais eficiente e confiável. Esse processo reforça a qualidade do software e a confiança na entrega contínua de funcionalidades estáveis.

## 📚 Referências:

FOWLER, Martin. Unit Test. 2014. Disponível em: https://martinfowler.com/bliki/UnitTest.html. Acesso em: 7 nov. 2024.

AMAZON. What is Unit Testing? Disponível em: https://aws.amazon.com/what-is/unit-testing/. Acesso em: 20 nov. 2024.

FOWLER, Martin. Given-When-Then. Disponível em: https://martinfowler.com/bliki/GivenWhenThen.html. Acesso em: 22 nov. 2024.

MICROSOFT. Unit test basics. Disponível em: https://learn.microsoft.com/en-us/visualstudio/test/unit-test-basics?view=vs-2022. Acesso em: 22 nov. 2024.
