# Técnica de Arquitetura: Transações

## Atributo de Qualidade 
Disponibilidade 

## Grupo, Subgrupo e Técnica
- Grupo de Técnicas: Prevenir Falhas
- Subgrupo: —
- Técnica: Transações
- Sub-técnica: —

### Descrição da Técnica 
A técnica de Transações é aplicada em sistemas distribuidos para garantir que as mensagens assíncronas trocadas entre componentes sejam processadas de maneira atômica, consistente, isolada e durável -- princípios conhecidos como propriedade **ACID**. 

Essa técnica visa evitar inconsistência e falhas que possam comprometer a **disponibilidade** do sistema, principalmete em ambientes onde vários serviços interagem de forma assíncrona e concorrente. 

Uma das principais implementaçoes dessa ténica é o **protocolo de commit em duas fases**, conhecidos como **TWO-PHASE COMMIT(2PC)** 

### Funcionamento do 2PC (Two-Phase Commit)
O 2PC é um protocolo que garante que **todas as partes envolvidas em uma transação** concordem com a operação antes de executá-la. Ele ocorre em duas etapas: 

1. Fase de Preparação: 
  * O coordenador da transação envia uma solicitação de "prepare-se para confirmar" para todos os participantes. 
  * Cada participante executa a operação localmente, mas não confirma, apenas sinaliza se está ponto para commit. 
  
2. Fase de Commit:
  * Se todos os participantes responderem positivamente, o coordenador envia um comando de "commit".
  * Caso algum participante informe falha, todos recebem um comando de "rollback".
Este processo evita que apenas parte da transação seja concluída, mantendo o sistema consistente mesmo em situações de falha parcial.

### Entendimento e Aplicação
A técnica de Transações é fundamental para sistemas que necessitam de alta disponibilidade e consistência de dados, como bancos, sistemas de pagamento, plataformas de e-commerce e aplicações corporativas com múltiplos microsserviços.

Ao garantir que uma transação só será confirmada se todos os envolvidos estiverem prontos, a técnica evita cenários de corrupção de dados ou perda de integridade, como:
  * Dois usuários comprando o último item em estoque ao mesmo tempo.
  * Processamento parcial de transferências bancárias.
  * Atualizações simultâneas em sistemas de registros compartilhados.

Apesar de adicionar uma camada de complexidade e possíveis impactos na latência, a segurança e a previsibilidade oferecidas pelas transações superam os custos em cenários críticos.