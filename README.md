# Revelador de respostas para Khan Academy

  *Funcionando a partir de 16/03/2023* 

Se este script ajudou ou te interessou, por favor, considere dar uma estrela no repositório acima. Esse número fica legal quando é grande.

## Uso
1. Baixe um gerenciador de userscripts como [TamperMonkey para Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=pt) ou [Greasemonkey para Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/greasemonkey/).
2. Use [este link](https://github.com/icfrancos/khanacademybot/blob/main/revealer.js) para instalar o script. 
3. Clique na extensão enquanto estiver no Khan Academy e certifique-se de que tanto a extensão quanto o script estão ativados.
4. Abra as Ferramentas de Desenvolvedor e vá para a aba Console. O script irá registrar no console as respostas à medida que o navegador as recebe.

## Dicas
- Khan Academy sempre solicita a pergunta atual e a próxima, então **espere que a penúltima mensagem no console seja a resposta correta**
- Quando há várias respostas, preencha as caixas da esquerda para a direita e depois para baixo. Você também pode pressionar tab para ir para o próximo campo. Exemplo abaixo
  - resposta: `[1, 2, 3, 4]`  pergunta: <img src="readme/multiple_free_response.png" width="250">
- Altere o nível de log do console para apenas **info** para uma experiência muito melhor
<img src="readme/console_log_level.jpg">

## Problemas Conhecidos
- Isso funciona apenas para perguntas de expressão, resposta livre, múltipla escolha e dropdown.
- O script fará o seu melhor para encontrar a resposta nos dados da pergunta, mas algumas perguntas de casos extremos não seguem a mesma estrutura, portanto não posso contê-las. (leia abaixo para entender a exploração)
- Se o script falhar para um determinado tipo de pergunta, abra um problema e eu darei uma olhada.
- Eu sou preguiçoso, portanto isso é cheio de bugs. Não se surpreenda quando você encontrar uma pergunta que você realmente terá que fazer

## Exploração
É bem simples. Em cada 'quiz' que você abre no aplicativo, seu navegador faz uma solicitação para `/getAssessmentItem`. O servidor responde com tudo o que seu cliente precisa para desenhar **e avaliar** sua pergunta. Dentro desta resposta graphql está um blob json contendo uma lista de perguntas, a maioria delas com um atributo `correct: boolean`. Às vezes, eles tentam te confundir colocando `correct` como o valor de uma chave rotulada como `status` ou `considered`.

## Implementação
Eu escrevi isso para Chrome, embora tudo deva funcionar no Gecko. Ele basicamente se conecta ao `fetch` do navegador, que é o que Khan Academy usa agora em vez de `XMLHttpRequest` (por isso alguns exploits antigos não funcionam mais, juntamente com a mudança de endpoint), e quando `/getAssessmentItem` é solicitado, ele registra a parte "importante" da resposta.

## Contribuição
Isso é totalmente open source! Se você quiser tentar automatizar este script, ou se quiser adicionar suporte para mais tipos de perguntas, como correspondência por exemplo, sinta-se à vontade para enviar um pull request. Eu farei questão de te creditar adequadamente!

## Licença
Isso tem a licença GNU GPL 3.0. Eu espero que a maioria dos usuários sejam pessoas como eu que têm tarefas de AP Stats e nenhuma vontade de fazê-las. Não me importo muito com o que você faz com isso, mas eu gosto de crédito :)
