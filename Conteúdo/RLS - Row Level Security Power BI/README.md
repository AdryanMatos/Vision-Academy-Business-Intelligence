
<div align="center">
  <h1>Acesso Inteligente com RLS</h1>
</div>
<h2>O que você vai aprender</h2>

Ao final deste tutorial, você será capaz de:

- 1️⃣ Compreender por que o Row-Level Security (RLS) é essencial para a segurança e governança de dados
- 2️⃣ Entender a diferença entre RLS estático e RLS dinâmico
- 3️⃣ Modelar tabelas de usuários e permissões para controle de acesso por linha
- 4️⃣ Configurar corretamente os relacionamentos entre tabelas no Power BI
- 5️⃣ Criar regras de RLS dinâmico utilizando DAX
- 6️⃣ Testar e validar perfis de acesso no Power BI Desktop
- 7️⃣ Publicar o relatório e configurar a segurança no Power BI Service


<h2>1️⃣ Por que RLS é necessário?</h2>

Imagine um relatório de vendas usado por vendedores, gerentes e diretoria.

- Cada vendedor deve ver apenas suas vendas.
- Cada gerente deve ver apenas sua região. 
- A diretoria pode ver tudo. 

Sem RLS, todos veriam todos os dados, o que gera:

- Risco de vazamento de informações.
- Falta de conformidade (LGPD / governança).
- Quebra de hierarquia organizacional.

<h2>2️⃣ RLS estático vs RLS dinâmico</h2>

No Power BI, o Row-Level Security (RLS) pode ser implementado de duas formas: estática ou dinâmica. A escolha entre elas impacta diretamente a manutenção, escalabilidade e governança do relatório.

No RLS estático, as regras de segurança são fixas e definidas diretamente na função, normalmente filtrando valores específicos.
 
```DAX
Exemplo:
Região = "Sul"
```

No RLS dinâmico, as regras se adaptam automaticamente com base no usuário logado, utilizando funções como USERPRINCIPALNAME() ou USERNAME().

```DAX
Exemplo: 
[AcessoEmail] = USERNAME()
```

<h2>3️⃣ Modelar tabelas de usuários e permissões para controle de acesso por linha</h2>

Para que o Row-Level Security (RLS) funcione corretamente, é fundamental que o modelo de dados contenha uma estrutura clara de usuários, permissões e relacionamentos. Essa modelagem é o que permite que o Power BI filtre os dados automaticamente conforme o usuário logado.

A solução é baseada em duas camadas principais:

- Tabela de usuários / acessos: Responsável por armazenar quem é o usuário e quais dados ele pode acessar.
- Tabela de fatos: Contém os dados que devem ser protegidos (ex.: vendas, acessos, indicadores).


<h3>Tabela de usuários / acessos:</h3> 

Essa tabela funciona como uma tabela de controle de permissões.

<img width="514" height="658" alt="image" src="https://github.com/user-attachments/assets/28975bc4-7224-40c2-b36d-70e45e568b98" />

<h3> Tabela de fatos (dados protegidos)</h3> 

A tabela de fatos contém os registros que devem ser filtrados dinamicamente.

<img width="1133" height="999" alt="image" src="https://github.com/user-attachments/assets/cafd4233-1620-48c3-85c9-131aff1b42fe" />

<h2> 4️⃣ Relacionamentos </h2> 

Para que o RLS funcione corretamente, é necessário criar um relacionamento entre: Tabela_Acessos → Tabela_Fatos

Cardinalidade: 1 → N

Direção do filtro: da tabela de Acessos para a tabela de Fatos

O filtro aplicado na tabela de Vendedores se propaga automaticamente para os dados.

<img width="565" height="444" alt="image" src="https://github.com/user-attachments/assets/1b9566da-06f0-4f2c-a17f-3c3fe926c637" />

<h2> 5️⃣ Criar regras de RLS dinâmico utilizando DAX </h2> 

Após a modelagem das tabelas de usuários e permissões, o próximo passo é criar as regras de Row-Level Security (RLS) dinâmico utilizando DAX. Essas regras são responsáveis por aplicar os filtros de acesso automaticamente, com base no usuário logado no Power BI.

<h3> Conceito do RLS dinâmico </h3> 

No RLS dinâmico, o filtro não é fixo. Ele é avaliado em tempo de execução, considerando:

- O usuário que acessa o relatório
- As permissões registradas na tabela de usuários
- Os relacionamentos do modelo

<img width="643" height="262" alt="image" src="https://github.com/user-attachments/assets/20f4c70d-a8c4-4a27-9090-f2b6d60adba2" />

<h3> Conceito do RLS fixo </h3> 

O Row-Level Security (RLS) fixo, também conhecido como RLS estático, é uma abordagem de segurança em que as regras de acesso são pré-definidas e não variam conforme o usuário logado. Nesse modelo, cada regra limita o acesso a um conjunto específico de dados, independentemente de quem esteja acessando o relatório.

No RLS fixo:

- As regras são criadas diretamente nas funções
- Os filtros aplicados são constantes
- Os usuários são vinculados manualmente a cada função

<img width="631" height="250" alt="image" src="https://github.com/user-attachments/assets/26744d3a-d71c-468d-bef7-378fa7a111aa" />

<h2> 6️⃣ Testar e validar perfis de acesso no Power BI Desktop </h2> 

```DAX
Modelagem → Exibir como
```

Após criar as regras de Row-Level Security (RLS), é essencial testar e validar os perfis de acesso antes de publicar o relatório. Essa etapa garante que cada usuário visualize apenas os dados permitidos, evitando falhas de segurança.

Passo a passo para testar

- Acesse o menu Modelagem
- Clique em Exibir como
- Selecione a role de RLS criada
- (Opcional) Informe um email para simular o usuário
- Confirme a simulação

O relatório será recarregado aplicando as regras de segurança selecionadas.

<img width="540" height="346" alt="image" src="https://github.com/user-attachments/assets/5acbd71f-fb77-4296-8968-14b615a3e693" />

<h2> 7️⃣ Publicar o relatório e configurar a segurança no Power BI Service </h2> 

Após testar e validar as regras de Row-Level Security (RLS) no Power BI Desktop, o próximo passo é publicar o relatório e configurar a segurança no Power BI Service. É somente no Service que o RLS passa a funcionar com usuários reais.

No Power BI Service:

- Acesse o workspace
- Clique nos três pontos (...) do dataset
- Selecione Segurança


Dentro da tela de segurança:

- Selecione a função criada (ex.: RLS por Vendedor)

Adicione:

- Usuários individuais (email)
- Ou grupos de segurança do Microsoft Entra ID (Azure AD)
- Salve as alterações
- O Power BI aplicará automaticamente as regras de RLS quando o usuário acessar o relatório.

<img width="696" height="275" alt="image" src="https://github.com/user-attachments/assets/dd42ea15-5fcf-4ad4-9df6-8f2d046d9784" />


<h2>⭐ Suporte</h2>

Gostou do material? Não esqueça de deixar uma **estrela** ⭐ no repositório!

Se quiser incentivar a criação de mais conteúdos gratuitos, você pode contribuir por aqui:
[💙 Clique para Apoiar o Projeto](https://nubank.com.br/cobrar/15oae1/695e72ce-de11-494f-9405-f7c3a3466ac0)
