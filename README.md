### Prompt de Produção Avançado: App "Modo Festa" (Legislação BR & Motor de Cálculo)

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
*   **Indicador de Tendência**: Seta indicando se o álcool está em curva de subida (absorção gástrica activa) ou descida (metabolização).
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

### 4\. SCRIPT DO MOTOR DE CÁLCULO (IMPLEMENTAÇÃO COMPLETA)

Implemente a lógica de cálculo em segundo plano utilizando a seguinte referência JavaScript/TypeScript para atualizar o estado global do app a cada 60 segundos ou a cada novo input:

typescript

    interface UserProfile {
      weightKg: number;
      gender: 'male' | 'female';
      isDriving: boolean;
    }
    
    interface LogEvent {
      timestamp: Date;
      type: 'alcohol' | 'food';
      volumeMl?: number;
      alcoholPercentage?: number; // Ex: 0.05 para 5%
      foodType?: 'snack' | 'meal';
    }
    
    function calculateAlcoolemia(profile: UserProfile, logs: LogEvent[]): { 
      bacMgL: number; 
      status: 'safe' | 'infraction' | 'crime';
      timeToSoberHours: number;
    } {
      if (logs.length === 0) return { bacMgL: 0, status: 'safe', timeToSoberHours: 0 };
    
      const now = new Date();
      const firstLogTime = new Date(logs[0].timestamp);
      const totalHoursElapsed = (now.getTime() - firstLogTime.getTime()) / (1000 * 60 * 60);
    
      // 1. Calcular total de álcool ingerido em gramas
      let totalAlcoholGrams = 0;
      let absorptionDelayMinutes = 0;
    
      logs.forEach(log => {
        if (log.type === 'alcohol' && log.volumeMl && log.alcoholPercentage) {
          // Gramas de álcool = Volume (ml) * (Teor / 100) * Densidade do Álcool (0.8)
          totalAlcoholGrams += log.volumeMl * log.alcoholPercentage * 0.8;
        } else if (log.type === 'food') {
          // Alimentos atrasam o pico de absorção
          absorptionDelayMinutes += log.foodType === 'meal' ? 45 : 20;
        }
      });
    
      // Ajusta o tempo decorrido considerando o atraso de absorção gástrica
      const adjustedHours = Math.max(0, totalHoursElapsed - (absorptionDelayMinutes / 60));
    
      // 2. Coeficiente de distribuição de água (r) e Taxa de eliminação (Beta)
      const r = profile.gender === 'male' ? 0.68 : 0.55;
      const betaPerHour = 0.015; // g/% por hora no sangue
    
      // 3. Fórmula de Widmark (Concentração de Álcool no Sangue em g/L)
      let bacGramPerLiterSangue = (totalAlcoholGrams / (r * profile.weightKg)) - (betaPerHour * adjustedHours);
      bacGramPerLiterSangue = Math.max(0, bacGramPerLiterSangue);
    
      // 4. Conversão Brasileira para Ar Alveolar (mg/L do Bafômetro)
      // A lei brasileira adota a relação de equivalência aproximada de 1 g/L de sangue = 0.45 a 0.5 mg/L de ar
      const bacMgL = Number((bacGramPerLiterSangue * 0.45).toFixed(2));
    
      // 5. Definição de Status Legal com base no CTB brasileiro
      let status: 'safe' | 'infraction' | 'crime' = 'safe';
      
      if (profile.isDriving && bacMgL > 0) {
        status = 'infraction'; // Tolerância zero se marcou que vai dirigir
      }
      
      if (bacMgL >= 0.05 && bacMgL <= 0.33) {
        status = 'infraction'; // Art. 165 CTB
      } else if (bacMgL >= 0.34) {
        status = 'crime';      // Art. 306 CTB
      }
    
      // 6. Estimativa de tempo para zerar (Sóbrio)
      const timeToSoberHours = bacGramPerLiterSangue > 0 ? Number((bacGramPerLiterSangue / betaPerHour).toFixed(1)) : 0;
    
      return { bacMgL, status, timeToSoberHours };
    }
    

Use o código com cuidado.

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
