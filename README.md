### Prompt de Produção Avançado: App "Modo Festa" (Legislação BR)

Crie um aplicativo web full-stack profissional, responsivo (mobile-first) e esteticamente impecável chamado "Modo Festa", focado em redução de danos, conscientização e monitoramento preditivo de alcoolemia.

O design deve seguir uma linha moderna "Dark Mode Premium", utilizando componentes limpos, gráficos fluidos e microinterações.

* * *

### 1\. POLÍTICA DE ISENÇÃO DE RESPONSABILIDADE (TERMOS DE USO MANDATÓRIOS)

*   **Onboarding Bloqueado**: Logo no primeiro acesso, o app deve exibir um modal em tela cheia (Overlay) intransponível. O usuário precisa rolar o texto até o fim para liberar o botão "Li e Aceito os Termos".
*   **Texto de Compliance e Aviso Legal**:
    
    > "AVISO LEGAL (DISCLAIMER): Este aplicativo é uma ferramenta estritamente voltada para entretenimento, alertas estatísticos e redução de danos. O metabolismo do álcool é único para cada indivíduo. Os resultados gerados são estimativas matemáticas baseadas em médias e NÃO possuem validade legal, médica ou pericial, não substituindo bafômetros oficiais. Os desenvolvedores não se responsabilizam por decisões, acidentes, multas ou problemas criminais decorrentes do uso do app. A LEGISLAÇÃO BRASILEIRA PREVÊ TOLERÂNCIA ZERO. SE BEBER, NÃO DIRIJA."
    
*   **Presença Persistente**: Um banner fixo no rodapé de todas as telas deve conter o texto: *"App para fins de entretenimento e alertas baseados em médias estatísticas. Não dirija."*

* * *

### 2\. REGRAS DA LEI SECA BRASILEIRA (CTB) NO MOTOR DO APP

O aplicativo deve monitorar e aplicar estritamente os limites estabelecidos pelo Código de Trânsito Brasileiro (CTB):

*   **Zona de Tolerância de Equipamento (≤ 0,04 mg/L)**: Interface limpa. Avisar que qualquer consumo posterior quebrará a margem de erro regulamentar do bafômetro.
*   **Zona de Infração Administrativa (≥ 0,05 mg/L a 0,33 mg/L)**: Ao atingir essa estimativa (Art. 165 do CTB), a interface deve disparar um aviso visual impeditivo e travá-lo na tela. Exibir mensagem em destaque: *"VOCÊ ESTÁ IMPEDIDO DE DIRIGIR. Risco de multa gravíssima de R$ 2.934,70 e suspensão da CNH por 12 meses."*
*   **Zona de Crime de Trânsito (≥ 0,34 mg/L)**: Ao atingir essa estimativa (Art. 306 do CTB), o app entra em Modo de Emergência. Exibir aviso piscante em vermelho: *"ALERTA CRÍTICO: Conduzir veículo neste estado configura CRIME DE TRÂNSITO sujeito a prisão/detenção de 6 meses a 3 anos."*

* * *

### 3\. COMPONENTES DA INTERFACE DE USUÁRIO (UI/UX)

### Tela de Configuração Inicial (Setup)

*   Formulário com inputs estilizados para: **Peso (kg)** e **Altura (cm)**.
*   Seletor de **Gênero Biológico** (necessário para o coeficiente metabólico de Widmark).
*   **Seletor de Objetivo da Noite**: Buttons cards selecionáveis (ex: "Apenas socializar" ou "Tolerância Zero/Vou Dirigir").
    *   *Nota de Código*: Se o usuário marcar "Vou Dirigir", o limite do app é fixado em 0.0 mg/L imediatamente. Qualquer adição de bebida altera o status do app para "Impedido de dirigir", sugerindo rotas de transporte alternativo.

### Dashboard Principal (Live Session)

*   **Radial Progress / Gauge Chart**: Gráfico circular animado que mostra a taxa estimada de álcool no sangue convertida para mg/L (miligramas por litro de ar alveolar).
*   **Indicador de Tendência**: Seta indicando se o álcool está em curva de subida (absorção gástrica ativa) ou descida (metabolização).
*   **Feed de Alertas Dinâmicos**: Cards que mudam de cor (Verde para seguro, Amarelo para atenção, Vermelho para Impedido de Dirigir).
*   **Botão de Resgate de Mobilidade**: Sempre que o usuário passar de 0,04 mg/L, exiba um botão proeminente: *"Chamar Carro por Aplicativo (Uber/99)"*.

### Grade de Inputs de Ação Rápida

*   **Módulo Bebidas**: Botões grandes com ícones vetoriais elegantes para:
    *   *Chopp/Cerveja Clara* (350ml - 4.7%)
    *   *Latão Premium/Cerveja Forte* (473ml - 5.5%)
    *   *Caipirinha/Cocktail* (200ml - 12%)
    *   *Shot Destilado* (50ml - 40%)
*   **Módulo Alimentação**: Botão rápido "Registrar Alimento" com opções para "Petiscos/Gorduras" ou "Refeição Completa".

* * *

### 4\. MOTOR DE CÁLCULO (WIDMARK REFINADO)

*   Use a Fórmula de Widmark Modificada: 
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)𝐵𝐴𝐶
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)\=𝐴𝑟×𝑊
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)−
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)(
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)𝛽
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)×𝑡
    
    ![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==))
    
    *   A = Massa de álcool puro consumida em gramas (Volume em ml × Teor Alcoólico × 0.8 de densidade).
    *   r = Fator de distribuição de água (0.68 para homens, 0.55 para mulheres).
    *   W = Peso corporal em gramas.
    *   β = Taxa de eliminação do fígado (Média de 0.015g/% por hora).
*   **Conversão para Bafômetro (Ar Alveolar)**: Divida o resultado de BAC por 2 para aproximar a leitura g/L de sangue para mg/L de ar expirado, alinhando com a escala dos bafômetros brasileiros.
*   **Fator Estômago Cheio**: Caso o usuário registre alimentação, atrase o pico de absorção do álcool no código em 45 minutos no cálculo da curva, simulando o retardo do esvaziamento gástrico.

* * *

### 5\. ARQUITETURA DE BANCO DE DADOS (SUPABASE INTEGRATION)

*   Tabela `user_sessions`: Armazena o perfil ativo, parâmetros biométricos e se o usuário marcou a opção de dirigir.
*   Tabela `consumption_logs`: Registra `id`, `session_id`, `timestamp`, `log_type` ('alcohol' ou 'food'), `alcohol_grams`, e `water_intake_ml`.

* * *

### 6\. SIMULADOR DE TELEMETRIA IOT (MODO ENGENHARIA)

*   No menu lateral ou rodapé, crie uma área expansível chamada "Sensores IoT (Protótipo)".
*   Inclua dois sliders de simulação para testar o sistema como se estivesse recebendo dados reais de hardware:
    1.  *Simulador de Copo Bluetooth*: Um botão para enviar um payload simulado de decréscimo de peso do copo (Ex: "Envio de evento: 150ml consumidos de Cerveja").
    2.  *Simulador de Smartwatch*: Um slider para alterar os Batimentos Cardíacos (BPM). Se o BPM simulado subir acima de 100 em repouso após um consumo, mude o status do app para "Aceleração metabólica detectada".
