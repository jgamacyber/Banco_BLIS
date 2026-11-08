# Caso Banco BLIS

Estudo de caso interativo sobre segurança e direito no uso de modelos da família BERT. Foi feito para fechar as apresentações do seminário de IA e PLN do BLIS (DTI BR).

**Acesse:** https://jgamacyber.github.io/Banco_BLIS/

## A história

O Banco BLIS é um banco fictício. O nome é uma homenagem ao laboratório, não uma instituição real. O SAC do banco usa dois modelos:

- **BLIS-Anon**, um BERT-CRF que troca nomes, CPFs, telefones e valores por marcadores antes de o texto sair do banco.
- **BLIS-Triagem**, um BERTimbau com pré-treino adaptado (TAPT) e ajuste fino, que manda cada reclamação para a fila certa. É retreinado todo mês e entra em produção sem revisão humana, desde que a acurácia geral não caia mais de 0,5 ponto.

Um anotador terceirizado troca 600 rótulos de "Fraude/golpe" para "Dúvida geral". O retreino aprova o modelo novo, e os golpes de falsa central passam a esperar 5 dias úteis em vez de 24 horas. Ninguém invadiu o sistema. Além disso, o anonimizador deixa passar nomes em minúsculas e CPFs com espaços, e esses dados vão parar num fornecedor nos Estados Unidos.

Os alunos assumem um de três papéis (Segurança, Jurídico ou Diretoria), investigam o caso e decidem o que fazer.

## Como usar

É um único arquivo `index.html`, sem dependências e sem servidor. Funciona aberto direto no navegador ou publicado no GitHub Pages.

| Endereço | Para quem | O que muda |
|---|---|---|
| `.../` | alunos | escolha de papel e botões de copiar o voto para o chat |
| `.../?modo=apresentador` | quem conduz | cronômetro por parte, navegação pelas setas do teclado e respostas atrás de "Mostrar resposta" |
| `.../?modo=revisao` | estudo prévio | todas as respostas já abertas |

Sem servidor, os votos vão pelo chat da aula. O aluno clica em "Copiar voto para o chat" e cola uma linha como `[JUR] Ato 1: B`.

## Roteiro (20 min)

| Parte | Tempo | O que acontece |
|---|---|---|
| Cenário e pipeline | 2 min | apresentação do banco, escolha dos papéis e comparação do modelo v12 com o v13 no simulador |
| Ato 1: detecção | 5 min | trilha de anotação, auditoria dos exemplos de treino e votação: é incidente de segurança? |
| Ato 2: responsabilidade | 6 min | vazamento pelo anonimizador, votação sobre quem responde ao cliente e uma pergunta para cada papel |
| Ato 3: controles | 5 min | cada aluno propõe um controle e a turma compara com a lista de referência |
| Fechamento | 2 min | duas ideias para levar |

## O simulador

A seção "Pipeline do SAC" mostra o caminho de quatro reclamações fictícias:

1. **Anonimização:** o texto que sai para o serviço de resumo, com as entidades trocadas por marcadores.
2. **Classificação:** a probabilidade de cada fila no modelo de outubro (v12) e no de novembro (v13).
3. **Fila:** o carimbo com a fila e o prazo de atendimento.

Ao ligar "Mostrar auditoria", aparecem os exemplos de treino reetiquetados e as entidades que o anonimizador não detectou.

## Artigos que originaram o caso

- Devlin et al. (2019). [BERT](https://arxiv.org/abs/1810.04805)
- Souza, Nogueira e Lotufo (2019). [Portuguese Named Entity Recognition using BERT-CRF](https://arxiv.org/abs/1909.10649)
- Souza, Nogueira e Lotufo (2020). [BERTimbau](https://link.springer.com/doi/10.1007/978-3-030-61377-8_28), BRACIS 2020
- Sun et al. (2019). [How to Fine-Tune BERT for Text Classification?](https://arxiv.org/abs/1905.05583)
- Chalkidis et al. (2020). [LEGAL-BERT](https://arxiv.org/abs/2010.02559)
- Gururangan et al. (2020). [Don't Stop Pretraining](https://arxiv.org/abs/2004.10964)
- Liu et al. (2019). [RoBERTa](https://arxiv.org/abs/1907.11692)
- Sanh et al. (2019). [DistilBERT](https://arxiv.org/abs/1910.01108)
- Rogers, Kovaleva e Rumshisky (2020). [A Primer in BERTology](https://arxiv.org/abs/2002.12327)
- Carmo et al. (2020). [PTT5](https://arxiv.org/abs/2008.09144)
- Ribeiro et al. (2020). [CheckList](https://arxiv.org/abs/2005.04118), citado nos controles

A página traz uma caixa "Onde cada artigo do seminário aparece no caso", com a ligação de cada artigo com a história.

## Normas citadas

- LGPD (Lei nº 13.709/2018), arts. 20, 33, 46 e 48
- Resoluções CD/ANPD nº 15/2024 (comunicação de incidentes) e nº 19/2024 (transferência internacional)
- CDC (Lei nº 8.078/1990), art. 14, e Súmulas 297 e 479 do STJ
- Resolução CMN nº 4.893/2021, com as alterações da Resolução CMN nº 5.274/2025
- PL 2.338/2023 (projeto de lei de IA, ainda em tramitação)

As normas foram conferidas em novembro de 2026. O material serve para discussão em aula e não é parecer jurídico.

## Publicar no GitHub Pages

1. Coloque o `index.html` na raiz do repositório.
2. Em **Settings > Pages**, escolha a branch `main` e a pasta `/ (root)`.
3. Espere um ou dois minutos e acesse `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.

## Privacidade

- Nenhum dado sai do navegador. A página guarda no `localStorage` só o papel escolhido e um identificador aleatório.
- Nomes, CPFs, telefones e relatos são inventados.
- A internet só é usada para carregar as fontes do Google Fonts. Sem conexão, a página usa a fonte do sistema.

## Servidor opcional

Se a página estiver no mesmo endereço de um servidor que responda em `api/saude`, ela passa a enviar os votos para lá e mostra o placar ao vivo no modo apresentador. Sem servidor, tudo continua funcionando pelo chat.

## Autores

Jaime de M. Gama da Silva, Beatriz Chieffi Failla e Rômulo Santos, para o Seminário de Inteligência Artificial e Processamento de Linguagem Natural do BLIS (DTI BR), novembro de 2026.
