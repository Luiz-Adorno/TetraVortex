# Tetra Vortex

**Tetra Vortex** é um Expert Advisor (EA) para MetaTrader 5 (MT5) que combina duas estratégias de negociação automatizada, **Redemption** e **Devotion**, utilizando uma abordagem de *grid trading* com gradientes dinâmicos. O EA é projetado para operar em mercados financeiros, como Forex, índices ou commodities, com foco em gerenciamento rigoroso de risco e monitoramento visual por meio de um painel unificado.

## Funcionalidades

- **Estratégias Duplas**:
  - **Redemption** e **Devotion**: Duas estratégias independentes com parâmetros configuráveis, operando no mesmo símbolo com magic numbers distintos (`21` para Redemption, `22` para Devotion).
  - Baseadas em *grid trading*, com entradas automáticas quando o preço desvia de um preço de referência em ±0.44% (Redemption) ou ±0.45% (Devotion).
- **Grid Trading Dinâmico**:
  - Abre posições adicionais em intervalos de 0.25% (Redemption) ou 0.08% (Devotion) contra o movimento do preço, com até 10 gradientes por estratégia.
  - Suporta modo de validação de grades (`GRID_VALIDATION_POSITIVE`) para restringir novas grades a preços favoráveis.
  - Ajusta níveis de grade a favor do movimento do preço (trailing).
- **Gerenciamento de Risco**:
  - Take profit percentual por posição (0.5% para ambas as estratégias, configurável).
  - Metas diárias e mensais de lucro (R$1.000 e R$5.000) e perda (-R$300 para Redemption, -R$500 para Devotion), com zeragem automática ao atingi-las.
  - Threshold mensal (R$10.000) que bloqueia a negociação se o lucro mensal cair a zero após atingir o limite.
  - Meta diária combinada (R$2.000) que zera ambas as estratégias se atingida.
- **Painel Unificado**:
  - Exibe informações em tempo real: preço de referência, gradientes ativos, horários, posições, lucro/prejuízo diário e mensal, volumes de compra/venda, e status de bloqueio.
  - Inclui botão "Zerar Tudo" para fechar todas as posições e excluir ordens pendentes.
- **Horários de Operação**:
  - Negocia entre 10:00 e 18:10 (configurável), com zeragem automática no horário de encerramento.
- **Modo Debug**:
  - Registra eventos detalhados (ex.: abertura de posições, ativação de gradientes) no log do MT5.

## Pré-requisitos

- **Plataforma**: MetaTrader 5 (versão mais recente recomendada).
- **Ativos Suportados**: Configurável para Forex, índices, commodities ou outros ativos disponíveis no MT5.
- **Conta**: Conta de negociação (demo ou real) com corretora compatível com MT5.
- **VPS (opcional)**: Recomendado para operação contínua 24/7.
- **Dependências**: Nenhum software adicional necessário além do MetaTrader 5.

## Instalação

1. **Download do EA**:
   - Acesse o arquivo `TetraVortex.mq5` no repositório privado.
2. **Adicionar ao MetaTrader 5**:
   - Copie o arquivo `TetraVortex.mq5` para a pasta `MQL5/Experts` do MetaTrader 5.
   - No MetaTrader 5, abra o Navegador (Ctrl+N) e localize o EA na lista de Expert Advisors.
3. **Configuração**:
   - Arraste o EA para o gráfico do ativo desejado.
   - Ajuste os parâmetros no menu de configuração do EA (veja a seção abaixo).
4. **Habilitar Negociação Automatizada**:
   - Certifique-se de que a opção "Permitir Negociação Automatizada" está ativada no MetaTrader 5.

## Configuração dos Parâmetros

### Redemption Parameters
| Parâmetro                     | Descrição                                      | Valor Padrão |
|-------------------------------|------------------------------------------------|--------------|
| `InpMagicNumber_Red`          | Magic Number para identificar posições         | 21           |
| `InpStartTime_Red`            | Horário de início da negociação                | 10:00        |
| `InpZeroingTime_Red`          | Horário de zeragem das posições                | 18:10        |
| `InpFirstEntryPercentRange_Red` | Desvio % para primeira entrada                | 0.44         |
| `InpGridSizePercent_Red`      | Tamanho da grade em %                          | 0.25         |
| `InpFirstContractSize_Red`    | Tamanho do contrato inicial (lotes)            | 1.0          |
| `InpContractSizePerOpening_Red` | Tamanho do contrato por grade (lotes)         | 1.0          |
| `InpCurrency_Red`             | Moeda (BRL ou USD)                            | BRL          |
| `InpDailyProfitTarget_Red`    | Meta de lucro diário (BRL)                    | 1,000.0      |
| `InpDailyLossTarget_Red`      | Meta de perda diária (BRL, negativo)          | -300.0       |
| `InpMonthlyProfitTarget_Red`  | Meta de lucro mensal (BRL)                    | 5,000.0      |
| `InpMonthlyLossTarget_Red`    | Meta de perda mensal (BRL, negativo)          | -2,400.0     |
| `InpMonthlyMaxThreshold_Red`  | Threshold máximo mensal (BRL)                 | 10,000.0     |
| `InpDebugMode_Red`            | Ativa logs detalhados                         | false        |
| `InpGridValidationMode_Red`   | Modo de validação de grades                   | DEFAULT      |
| `InpTakeProfitPercent_Red`    | Take profit por posição (%)                   | 0.5          |

### Devotion Parameters
| Parâmetro                     | Descrição                                      | Valor Padrão |
|-------------------------------|------------------------------------------------|--------------|
| `InpMagicNumber_Dev`          | Magic Number para identificar posições         | 22           |
| `InpStartTime_Dev`            | Horário de início da negociação                | 10:00        |
| `InpZeroingTime_Dev`          | Horário de zeragem das posições                | 18:10        |
| `InpFirstEntryPercentRange_Dev` | Desvio % para primeira entrada                | 0.45         |
| `InpGridSizePercent_Dev`      | Tamanho da grade em %                          | 0.08         |
| `InpFirstContractSize_Dev`    | Tamanho do contrato inicial (lotes)            | 1.0          |
| `InpContractSizePerOpening_Dev` | Tamanho do contrato por grade (lotes)         | 1.0          |
| `InpCurrency_Dev`             | Moeda (BRL ou USD)                            | BRL          |
| `InpDailyProfitTarget_Dev`    | Meta de lucro diário (BRL)                    | 1,000.0      |
| `InpDailyLossTarget_Dev`      | Meta de perda diária (BRL, negativo)          | -500.0       |
| `InpMonthlyProfitTarget_Dev`  | Meta de lucro mensal (BRL)                    | 5,000.0      |
| `InpMonthlyLossTarget_Dev`    | Meta de perda mensal (BRL, negativo)          | -2,500.0     |
| `InpMonthlyMaxThreshold_Dev`  | Threshold máximo mensal (BRL)                 | 10,000.0     |
| `InpDebugMode_Dev`            | Ativa logs detalhados                         | false        |
| `InpGridValidationMode_Dev`   | Modo de validação de grades                   | DEFAULT      |
| `InpTakeProfitPercent_Dev`    | Take profit por posição (%)                   | 0.5          |

### Unified Panel Parameters
| Parâmetro                     | Descrição                                      | Valor Padrão |
|-------------------------------|------------------------------------------------|--------------|
| `InpShowUnifiedPanel`         | Ativa o painel unificado no gráfico            | true         |
| `InpPanelWidth`               | Largura do painel (pixels)                    | 400          |
| `InpPanelHeight`              | Altura de cada linha do painel (pixels)       | 32           |
| `InpCombinedDailyProfitTarget`| Meta de lucro diário combinado (BRL)          | 2,000.0      |

## Uso

1. **Backtesting**:
   - Use o Testador de Estratégias do MetaTrader 5 para avaliar o desempenho do EA.
   - Configure o período de teste, ativo, timeframe e parâmetros desejados.
   - Recomenda-se testar em diferentes condições de mercado para otimizar os parâmetros.

2. **Negociação ao Vivo**:
   - Aplique o EA em uma conta demo antes de usar em uma conta real.
   - Monitore o painel unificado para acompanhar o desempenho em tempo real.
   - Use o botão "Zerar Tudo" para fechar todas as posições manualmente, se necessário.

## Exemplo de Estratégia

O Tetra Vortex opera com base em uma estratégia de *grid trading* com gradientes dinâmicos:
- **Preço de Referência**: Definido como o preço de abertura do primeiro candle após o horário de início (10:00).
- **Entrada Inicial**:
  - **Redemption**: Compra quando o preço cai 0.44% abaixo do preço de referência; venda quando sobe 0.44%.
  - **Devotion**: Venda quando o preço cai 0.45% abaixo do preço de referência; compra quando sobe 0.45%.
- **Gerenciamento de Gradientes**:
  - A cada 0.25% (Redemption) ou 0.08% (Devotion) de movimento contra a posição inicial, uma nova posição é aberta (até 10 gradientes).
  - Se o preço se move a favor, o nível da grade é ajustado (trailing).
- **Fechamento**:
  - Posições são fechadas ao atingir metas de lucro/perda diárias ou mensais, no horário de zeragem (18:10), ou pelo botão "Zerar Tudo".
  - Take profit de 0.5% é aplicado a cada posição.

## Licença

Este projeto está licenciado sob a **MIT License**. Veja o arquivo `LICENSE` para mais detalhes.

## Aviso

A negociação automatizada envolve riscos financeiros significativos. Teste o EA em uma conta demo antes de usá-lo em uma conta real. O desenvolvedor não se responsabiliza por perdas financeiras resultantes do uso deste EA.

---

**© 2025 Tetra Vortex EA**
