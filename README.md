# Testes Unitários

## Definição

Segundo Martin Fowler, testes unitários são uma prática que visa testar pequenas partes do código de maneira isolada para verificar sua funcionalidade correta. Ele destaca as abordagens "solitária" e "sociável": a primeira simula dependências com mocks, enquanto a segunda permite interações entre componentes reais. É recomendado que os testes sejam rápidos e executados frequentemente para facilitar a detecção de erros logo após mudanças, promovendo assim qualidade e estabilidade no desenvolvimento contínuo.

![sociable-solitary](https://martinfowler.com/bliki/images/unitTest/isolate.png)

- Fonte: FOWLER, Martin. Unit Test. 2014. Disponível em: https://martinfowler.com/bliki/UnitTest.html. Acesso em: 7 nov. 2024.

## Testes no contexto do processo de desenvolvimento

No processo de desenvolvimento, os testes unitários são executados automaticamente quando ocorre um trigger, que, neste caso, é a abertura de um pull request.

### Fluxo:

1️⃣ O desenvolvedor escreve os testes durante o desenvolvimento da feature.

2️⃣ Após concluir a feature, o desenvolvedor abre um pull request para a branch `develop`, acionando o trigger.

3️⃣ Os testes unitários são executados automaticamente.
- Se algum teste falhar, o código retorna ao desenvolvedor para ajustes e correções. ❌
- Se todos os testes forem aprovados, o pull request é aceito e o código é integrado à branch `develop` via merge. ✅

## Exemplos práticos

### Testes unitários no back-end

A seguir estão exemplos de testes unitários implementados no back-end do Projeto Integrador que está sendo desenvolvido neste semestre.

<details open>
<summary>  
  <b> PermissaoUCTest </b>
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

Resultado:

![PermissaoUCTest](https://github.com/user-attachments/assets/8402e6e6-8bba-4f19-b345-c11411a07549)

</details>

<details open>
<summary>
  <b> GrupoUCTest </b>
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

![GrupoUCTest](https://github.com/user-attachments/assets/69c6a878-447c-4d40-8ddf-35199014185f)

</details>

## Tecnologias utilizadas:

![java](https://github.com/user-attachments/assets/99d67934-179e-4739-a998-7eb745f64222)
![spring](https://github.com/user-attachments/assets/5a371f1e-11e8-4685-840d-b20d7666bde8)
![junit](https://github.com/user-attachments/assets/3c14bef1-0146-4195-8515-d1fe7f788249)

