# ✨ Gerador de Prompts para Iniciantes

Ferramenta web de um único arquivo que transforma respostas simples em **prompts
bem estruturados**, prontos para colar em qualquer IA (Claude, ChatGPT, Gemini etc.).

Feita para quem **nunca estudou engenharia de prompts**: sem jargão, com exemplos
em cada campo, dicas em tempo real e um clique para copiar.

> Sem instalação, sem dependências, sem servidor. Basta abrir o arquivo no navegador.

---

## Sumário

- [Funcionalidades](#funcionalidades)
- [Como usar](#como-usar)
- [Modos disponíveis](#modos-disponíveis)
- [O que o prompt gerado contém](#o-que-o-prompt-gerado-contém)
- [Executar localmente](#executar-localmente)
- [Personalização](#personalização)
- [Privacidade](#privacidade)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

---

## Funcionalidades

| Recurso | Para que serve |
| --- | --- |
| **Perguntas em linguagem simples** | Troca termos técnicos por perguntas diretas, com exemplos nos campos. |
| **Campos essenciais primeiro** | Só o necessário aparece de início; o restante fica em uma seção opcional. |
| **Botões de escolha rápida** | Tom e formato da resposta podem ser escolhidos com um clique. |
| **Preencher com exemplo** | Mostra como um prompt bem preenchido fica. |
| **Medidor de qualidade** | Indica *Básico*, *Bom* ou *Excelente* e sugere o que falta. |
| **Prompt editável** | O texto gerado pode ser ajustado à mão antes de copiar. |
| **Proteção contra perda de edição** | Se você editou o texto, as mudanças nos campos só são aplicadas quando você clicar em **Atualizar com os campos**. |
| **Salvamento automático** | Os campos ficam guardados no navegador para você continuar depois. |
| **Tema claro e escuro** | Segue a preferência do sistema operacional. |
| **Responsivo e acessível** | Funciona em celular e desktop, com foco visível no teclado e suporte a leitores de tela. |

## Como usar

1. **Escolha** o que deseja fazer (escrever, pesquisar ou programar).
2. **Preencha** os campos. Apenas o primeiro, marcado com `*`, é obrigatório.
3. **Copie** o prompt e cole na sua IA favorita.

Dica: se a IA responder com perguntas, é intencional. O prompt pede que ela pergunte
antes de supor quando faltar algo essencial. Responda e o resultado melhora.

## Modos disponíveis

### ✍️ Escrever e planejar
Para e-mails, textos, planos e ideias.
Campos: tarefa, contexto, público, tom, formato e especialista (opcional).

### 🔎 Pesquisar e analisar
Para resumos, comparações e relatórios.
Campos: pergunta principal, público, **origem das informações**, material para analisar, período ou região e formato.

A origem das informações define as regras de evidência incluídas no prompt:

- **Conhecimento da IA:** a IA avisa quando tiver dúvida e separa fatos de interpretações.
- **Internet:** a IA cita fontes e confirma dados importantes. Exige que a IA usada
tenha busca ativada; se não tiver, ela é instruída a avisar em vez de simular
a pesquisa.
- **Somente o material fornecido:** a IA não usa conhecimento externo e sinaliza
o que não estiver no material.

### 💻 Programar
Para corrigir erros, criar ou explicar código.
Campos: problema, linguagem ou ferramenta, código ou erro, resultado esperado,
restrições e formato da resposta (por exemplo, “explicar passo a passo”).

## O que o prompt gerado contém

Os prompts seguem práticas consolidadas de engenharia de prompts:

- **Estrutura em Markdown** com seções claras (`# Tarefa`, `## Contexto`,
`## Formato da resposta` etc.).
- **Delimitadores XML** (`<material>`, `<codigo>`, `<contexto>`) para separar o
conteúdo colado das instruções. No material e no código são sempre usados; no contexto,
só quando o texto é longo ou tem várias linhas.
- **Pedido de esclarecimento:** a IA deve fazer até 3 perguntas objetivas se faltar
informação essencial.
- **Regras contra invenção:** a IA não deve inventar fatos, números, fontes, bibliotecas
ou resultados de testes.
- **Defesa contra instruções embutidas:** no modo de material fornecido, o conteúdo
colado é tratado como dado, não como comando.
- **Formato de entrega explícito**, definido pelo usuário ou com um padrão sensato.

<details>
<summary>Exemplo de prompt gerado (modo “Escrever e planejar”)</summary>

```markdown
Atue como gerente financeira especialista em relacionamento com clientes.

# Tarefa
Escrever um e-mail cobrando com educação uma fatura em atraso

## Contexto
Cliente há 2 anos. Fatura de R$ 1.200 venceu dia 10. Nunca atrasou antes.

## Público
Dono de uma pequena empresa, cliente nosso

## Tom
Amigável

## Formato da resposta
E-mail pronto, com assunto

## Como trabalhar
- Se faltar uma informação essencial, faça até 3 perguntas objetivas antes de responder.
- Não invente fatos, números, nomes ou prazos; sinalize o que estiver faltando.
- Entregue um resultado pronto para usar, em linguagem clara e direta.
```

</details>

## Executar localmente

Não há build nem dependências.

```bash
git clone https://github.com/squassina/PromptGen.git
cd PromptGen
```

Depois, abra `index.html` com um duplo clique ou, se preferir um servidor local:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000/index.html
```

## Personalização

Todo o conteúdo dos formulários está em um único objeto JavaScript, `M`, no início
do `<script>`. Para ajustar textos, campos, exemplos ou opções, edite esse objeto:

```js
{
  id: 'tone',                  // identificador do campo
  l: 'Qual tom você prefere?', // rótulo exibido
  h: 'Opcional.',              // texto de ajuda (opcional)
  req: 1,                      // campo obrigatório
  area: 1,                     // usa textarea em vez de input
  adv: 1,                      // aparece na seção opcional
  chips: ['Amigável', 'Direto'], // botões de escolha rápida
  ph: 'Ex.: ...',              // placeholder
  tip: 'escolha um tom'        // dica do medidor de qualidade
}
```

Para mudar o texto do prompt gerado, edite a função `build()` e o objeto `SRC`
(regras de evidência do modo pesquisa).

Para adicionar um novo modo, crie uma nova chave em `M` (com `n`, `d`, `fields`
e `ex`) e uma nova ramificação em `build()`.

## Privacidade

- Tudo roda **no seu navegador**. Nenhum texto é enviado a servidores.
- Os campos são salvos apenas no `localStorage` do seu próprio navegador
(chave `gp-v4`). Para apagar, use **Limpar campos** ou limpe os dados do site.
- A ferramenta não faz requisições de rede nem usa bibliotecas externas.
- Evite colar senhas, chaves de API ou dados sensíveis nos campos, principalmente
porque o prompt final será enviado à IA que você escolher.

## Estrutura do projeto

```text
.
├── index.html   # HTML, CSS e JavaScript em um único arquivo
└── LICENSE
└── README.md
└── README.BR.md
```

## Contribuindo

Contribuições são bem-vindas!

1. Faça um fork do projeto.
2. Crie uma branch: `git checkout -b minha-melhoria`.
3. Faça o commit: `git commit -m "Descreve a melhoria"`.
4. Envie: `git push origin minha-melhoria`.
5. Abra um Pull Request.

Ideias de melhoria: novos modos (marketing, educação, atendimento), exportação em
`.txt`, histórico de prompts, versão em outros idiomas e testes automatizados.

Ao propor mudanças, preserve o foco em **iniciantes**: linguagem simples, poucos
campos obrigatórios e dicas claras.

## Licença

Este projeto está sob a [Licença MIT](LICENSE).
