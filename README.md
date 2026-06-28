# Prompt de Produção Avançado: App "Modo Festa"

Crie um aplicativo web full-stack profissional, responsivo (mobile-first) e esteticamente impecável chamado "Modo Festa", focado em redução de danos, conscientização e monitoramento preditivo de alcoolemia. 

O design deve seguir uma linha moderna "Dark Mode Premium", utilizando componentes limpos, gráficos fluidos e microinterações.

---

### 1. POLÍTICA DE ISENÇÃO DE RESPONSABILIDADE (TERMOS DE USO)
* **Onboarding Mandatório**: Logo no primeiro acesso, antes de configurar o perfil, o app deve exibir um modal em tela cheia (Overlay) que o usuário precisa ler e rolar até o fim para aceitar.
* **Texto Legal e de Compliance**:
  > "AVISO LEGAL (DISCLAIMER): Este aplicativo é uma ferramenta de entretenimento, conscientização e redução de danos baseada em cálculos matemáticos estatísticos aproximados. O metabolismo do álcool varia drasticamente de indivíduo para indivíduo. Os dados exibidos NÃO substituem testes clínicos, bafômetros oficiais ou orientação médica. Os desenvolvedores e a plataforma NÃO se responsabilizam por quaisquer danos, decisões, acidentes ou problemas legais decorrentes do uso ou mau uso desta aplicação. SE BEBER, NÃO DIRIJA sob nenhuma circunstância."
* **Presença Persistente**: Um aviso discreto no rodapé de todas as telas principais deve conter o texto: *"App para fins de entretenimento e alertas baseados em médias estatísticas. Não dirija."*

---

### 2. COMPONENTES DA INTERFACE DE USUÁRIO (UI/UX PREMIUM)

#### Tela de Configuração Inicial (Setup)
* Formulário segmentado com inputs numéricos estilizados para: **Peso (kg)** e **Altura (cm)**.
* Seletor de **Gênero Biológico** (necessário para o coeficiente de Widmark).
* **Seletor de Objetivo da Noite**: Buttons cards selecionáveis (ex: "Ficar alegre/Apenas socializar" ou "Tolerância Zero/Vou Dirigir").
* Se o usuário marcar "Vou Dirigir", a interface muda o tema de acento para amarelo/vermelia de atenção e fixa o limite do app em 0.0 g/l.

#### Dashboard Principal (Live Session)
* **Radial Progress / Gauge Chart**: Um gráfico circular centralizado e animado que mostra a taxa estimada de álcool no sangue em g/L ou mg/L.
* **Indicador de Tendência**: Uma seta indicando se a alcoolemia está em curva de subida (absorção) ou descida (metabolização).
* **Feed de Alertas Dinâmicos**: Um card de destaque que muda de cor (verde, amarelo, vermelho) e exibe textos baseados no estado atual (Ex: *"Seu corpo está processando a última dose. Recomendação: Intercale com 300ml de água agora"*).
* **Contador de Tempo**: Cronômetro de tempo decorrido desde o início e estimativa de horário em que o usuário estará totalmente sóbrio (alcoolemia = 0.0).

#### Grade de Inputs de Ação Rápida (Large Touch Targets)
* **Módulo Bebidas**: Botões com ícones vetoriais elegantes para:
  * *Chopp/Cerveja Clara* (350ml - 4.7%)
  * *Latão Premium/Cerveja Forte* (473ml - 5.5%)
  * *Caipirinha/Cocktail* (200ml - 12%)
  * *Shot Destilado* (50ml - 40%)
* **Módulo Alimentação**: Botão de atalho "Registrar Alimento" com opções para "Petiscos/Gorduras" ou "Refeição Completa".

---

### 3. MOTOR DE CÁLCULO E LÓGICA DE PROGRAMAÇÃO (WIDMARK REFINADO)
* Use a Fórmula de Widmark Modificada: BAC = (A / (r * W)) - (Beta * t)
  * `A` = Massa de álcool puro consumida em gramas (Volume em ml * Teor Alcoólico * 0.8 de densidade).
  * `r` = Fator de distribuição de água corporal (Média de 0.68 para homens, 0.55 para mulheres).
  * `W` = Peso corporal em gramas (ou kg ajustado à fórmula).
  * `Beta` = Taxa de eliminação do fígado (Fixar na média conservadora de 0.015g/% por hora).
* **Fator Estômago Cheio**: Caso o usuário registre alimentação, atrase o pico de absorção do álcool no código em 45 minutos no cálculo da curva, simulando o retardo do esvaziamento gástrico.

---

### 4. ARQUITETURA DE BANCO DE DADOS (SUPABASE INTEGRATION)
* Crie uma tabela `user_sessions` para armazenar o perfil ativo e o plano da noite.
* Crie uma tabela `consumption_logs` relacionada, registrando `id`, `session_id`, `timestamp`, `log_type` ('alcohol' ou 'food'), `alcohol_grams`, e `water_intake_ml`.

---

### 5. SIMULADOR DE TELEMETRIA IOT (MODO ENGENHARIA)
* No menu lateral ou rodapé, crie uma área expansível chamada "Sensores IoT (Protótipo)".
* Inclua dois sliders de simulação para testar o sistema como se estivesse recebendo dados reais de hardware:
  1. *Simulador de Copo Bluetooth*: Um botão para enviar um payload simulado de decréscimo de peso do copo (Ex: "Envio de evento: 150ml consumidos de Cerveja").
  2. *Simulador de Smartwatch*: Um slider para alterar os Batimentos Cardíacos (BPM). Se o BPM simulado subir acima de 100 em repouso após um consumo, mude o status do app para "Aceleração metabólica detectada".
