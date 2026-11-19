# ChefOS — gestão de restaurantes

O ChefOS reúne a operação de restaurantes em uma plataforma que cobre atendimento, pedidos, cozinha, caixa e estoque. O problema é manter esses pontos da operação conectados quando a equipe trabalha em várias estações e dispositivos.

**Produto:** [chefos.online](https://chefos.online)

## Arquitetura

| Componente | Responsabilidade |
| --- | --- |
| Portal web | Interface de gestão e operação para a equipe do restaurante. |
| Core | Backend modular com PostgreSQL e contratos OpenAPI para os domínios da operação, como pedidos, caixa, estoque e produção. |
| Android | Aplicativo nativo em Kotlin e Jetpack Compose, com layout adaptativo para tablets e celulares e fluxos de mesas e comandas. |
| Edge | Piloto Windows para executar fluxos locais de PDV, cozinha e caixa com PostgreSQL local. |

## Decisões de engenharia

- **Organizar o backend por domínio.** Separar pedidos, produção e caixa permite evoluir seus contratos e regras com fronteiras explícitas.
- **Adaptar o PDV ao atendimento em tablet.** Em telas largas, o app pode exibir salão e conta ou catálogo e carrinho lado a lado.
- **Tratar respostas incertas no PDV.** Se o dispositivo perde a resposta após uma escrita, o app registra que houve uma tentativa. O fluxo evita reenviar automaticamente uma operação que pode já ter sido aplicada.
- **Validar a execução local como piloto.** O Edge permite exercitar o fluxo operacional em ambiente local. A homologação para restaurante, redes locais e funcionamento offline prolongado segue como etapa própria.

## Material público

O site apresenta o produto. O repositório Edge documenta o piloto, os requisitos de execução e os limites de validação. O código dos componentes operacionais tem acesso restrito.

[Site do ChefOS](https://chefos.online) · [Código e documentação do piloto Edge](https://github.com/koresolucoes/chefosEdge)
