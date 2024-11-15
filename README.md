# Testes Unitários

## Definição

Segundo Martin Fowler, testes unitários são uma prática que visa testar pequenas partes do código de maneira isolada para verificar sua funcionalidade correta. Ele destaca as abordagens "solitária" e "sociável": a primeira simula dependências com mocks, enquanto a segunda permite interações entre componentes reais. É recomendado que os testes sejam rápidos e executados frequentemente para facilitar a detecção de erros logo após mudanças, promovendo assim qualidade e estabilidade no desenvolvimento contínuo.

![sociable-solitary](https://martinfowler.com/bliki/images/unitTest/isolate.png)

- Fonte: FOWLER, Martin. Unit Test. 2014. Disponível em: https://martinfowler.com/bliki/UnitTest.html. Acesso em: 7 nov. 2024.

## Testes no contexto do processo de desenvolvimento

No processo de desenvolvimento os testes são rodados de forma automática após o trigger (quando é aberto um pull request) ser ativado.

O desenvolvedor escreve os testes durante o desenvolvimento da feature ➡️ Feature finalizada ➡️ É aberto um pull request para a branch develop (onde são rodados os testes unitários) ➡️ Se falhar, retorna para a correção. Se for aprovado, é realizado o merge com a branch develop.

## Exemplos práticos

### Testes unitários no back-end

A seguir temos alguns exemplos de testes unitários implementados no back-end do Projeto Integrador que estamos desenvolvendo neste semestre.

<details open>
<summary>
  
#### PermissaoUCTest

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
```
</details>

<details open>
<summary>
  
#### GrupoUCTest

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
</details>

