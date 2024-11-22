# Testes Unitários

## 📖 Definição

Segundo Martin Fowler, testes unitários são uma prática que visa testar pequenas partes do código para verificar sua funcionalidade correta. Ele destaca as abordagens "solitária" e "sociável": a primeira simula dependências com mocks, enquanto a segunda permite interações entre componentes reais. É recomendado que os testes sejam rápidos e executados frequentemente para facilitar a detecção de erros logo após mudanças, promovendo assim qualidade e estabilidade no desenvolvimento contínuo.

![abordagens-testes-unitarios](https://github.com/xxzidanilloxx/sakaue/blob/main/assets/abordagens-testes-unitarios.svg)

- Fonte: FOWLER, Martin. Unit Test. 2014. Disponível em: https://martinfowler.com/bliki/UnitTest.html. Acesso em: 7 nov. 2024.

## ⚙️ Testes unitários no contexto do processo de desenvolvimento

### Fluxograma:

![fluxograma-testes-unitarios](https://github.com/xxzidanilloxx/sakaue/blob/main/assets/fluxograma-testes-unitarios.svg)

> [!NOTE]
> No processo de desenvolvimento, os testes unitários são executados automaticamente quando ocorre um trigger, que, neste caso, é a abertura de um pull request.

## 💡 Exemplos práticos

A seguir estão exemplos de testes unitários implementados no Projeto Integrador que está sendo desenvolvido neste semestre.

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

### Back-end:

<div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/java.svg" alt="java" width="75" height="75">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/junit.svg" alt="spring" width="75" height="75">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/spring.svg" alt="junit" width="75" height="75">
</div>

### Front-end:

<div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/typescript.svg" alt="typescript" width="75" height="75">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/angular.svg" alt="angular" width="75" height="75">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/jasmine.svg" alt="jasmine" width="75" height="75">
  <img src="https://github.com/xxzidanilloxx/sakaue/blob/main/assets/karma.svg" alt="karma" width="75" height="75">
</div>

## 🎯 Conclusão

A prática de testes unitários proporciona uma descoberta eficiente de bugs, permitindo detectar erros de entrada, saída ou lógica em blocos de código antes que eles alcancem o ambiente de produção. Com o mesmo conjunto de testes sendo executado continuamente após alterações no código, é possível identificar falhas relacionadas a bugs de maneira ágil.

Além disso, os testes unitários aceleram a identificação de problemas, reduzindo o tempo gasto com depuração. Eles ajudam os desenvolvedores a localizar rapidamente a parte exata do código que apresenta o erro, promovendo um ciclo de desenvolvimento mais eficiente e confiável. Esse processo reforça a qualidade do software e a confiança na entrega contínua de funcionalidades estáveis.
