# Testes Unitários

## Definição

Segundo Martin Fowler, testes unitários são uma prática que visa testar pequenas partes do código de maneira isolada para verificar sua funcionalidade correta. Ele destaca as abordagens "solitária" e "sociável": a primeira simula dependências com mocks, enquanto a segunda permite interações entre componentes reais. É recomendado que os testes sejam rápidos e executados frequentemente para facilitar a detecção de erros logo após mudanças, promovendo assim qualidade e estabilidade no desenvolvimento contínuo.

![sociable-solitary](https://martinfowler.com/bliki/images/unitTest/isolate.png)

- Fonte: FOWLER, Martin. Unit Test. 2014. Disponível em: https://martinfowler.com/bliki/UnitTest.html. Acesso em: 7 nov. 2024.

## Testes unitários no contexto do processo de desenvolvimento

No processo de desenvolvimento, os testes unitários são executados automaticamente quando ocorre um trigger, que, neste caso, é a abertura de um pull request.

### Fluxo:

1️⃣ O desenvolvedor escreve os testes durante o desenvolvimento da feature.

2️⃣ Após concluir a feature, o desenvolvedor abre um pull request para a branch `develop`, acionando o trigger.

3️⃣ Os testes unitários são executados automaticamente.
- Se algum teste falhar, o código retorna ao desenvolvedor para ajustes e correções. ❌
- Se todos os testes forem aprovados, o pull request é aceito e o código é integrado à branch `develop` via merge. ✅

![fluxograma](https://github.com/user-attachments/assets/b04e4d73-c53d-4339-b575-8038799ddbfd)

## Exemplos práticos

A seguir estão exemplos de testes unitários implementados no Projeto Integrador que está sendo desenvolvido neste semestre.

### Testes unitários no back-end

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

Resultado:

![PermissaoUCTest](https://github.com/user-attachments/assets/d09e9991-37ce-4c19-b379-f9ac4a85467e)

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
    void deveListarTodosGrupos() {
        List<Grupo> resultado = grupoUC.listar();

        assertEquals(1, resultado.size());
        assertEquals("TESTE", resultado.get(0).getNome());
    }
}
```

Resultado:

![GrupoUCTest](https://github.com/user-attachments/assets/869c25b3-54ea-4ddd-ad7d-636b939a9115)

</details>

### Testes unitários no front-end

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

## Tecnologias utilizadas

![java](https://github.com/user-attachments/assets/99d67934-179e-4739-a998-7eb745f64222)
![spring](https://github.com/user-attachments/assets/5a371f1e-11e8-4685-840d-b20d7666bde8)
![junit](https://github.com/user-attachments/assets/3c14bef1-0146-4195-8515-d1fe7f788249)
![typescript](https://github.com/user-attachments/assets/09006569-9e06-40bc-bd81-3805ce4c0031)
![angular](https://github.com/user-attachments/assets/5b7c18f4-e3eb-4dea-9b0c-56f5c306da76)
![jasmine](https://github.com/user-attachments/assets/41a07017-0233-480d-a9d3-806c6a755312)

## Conclusão

A prática de testes unitários proporciona uma descoberta eficiente de bugs, permitindo detectar erros de entrada, saída ou lógica em blocos de código antes que eles alcancem o ambiente de produção. Com o mesmo conjunto de testes sendo executado continuamente após alterações no código, é possível identificar falhas relacionadas a bugs de maneira ágil.

Além disso, os testes unitários aceleram a identificação de problemas, reduzindo o tempo gasto com depuração. Eles ajudam os desenvolvedores a localizar rapidamente a parte exata do código que apresenta o erro, promovendo um ciclo de desenvolvimento mais eficiente e confiável. Esse processo reforça a qualidade do software e a confiança na entrega contínua de funcionalidades estáveis.
