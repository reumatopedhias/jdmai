# Calculadora JDMAI à beira do leito

Calculadora em português do Juvenile DermatoMyositis Activity Index (JDMAI1 e JDMAI2) para residentes de reumatologia pediátrica, com o exame físico organizado por postura do paciente. O dono do projeto é médico reumatologista pediátrico, não programador: explique em português, de forma simples, o que cada comando faz antes de rodá-lo.

## Estrutura
- `index.html`: página única (HTML + CSS + JS, sem dependências nem build). Abre direto no navegador.
- `img/`: fotos dos testes do MMT8, extraídas do manual NIEHS/IMACS "Manual Muscle Testing Procedures for MMT8 Testing" (2007). `*-ge.jpg` = posição sem gravidade.

## Lógica do cálculo (não alterar sem avisar e justificar)
Conferida com o app oficial do Istituto Giannina Gaslini (https://biodaas.gaslini.org/jdmai-app). Caso de teste: PhGA 2, PaGA 3, MMT8 com todos os grupos = 8, abdominais 6/6, elevação da cabeça 3, levantar do chão 6, VAS pele 4, DAS pele (eritema leve, focal, 2 sinais vasculares, Gottron moderado) → JDMAI1 = 12, JDMAI2 = 13.

- JDMAI1 = PhGA (0–10) + PaGA (0–10) + força (0–10) + VAS de pele do médico (0–10) → 0–40
- JDMAI2 = PhGA + PaGA + força + DAS pele (0–9) → 0–39
- VAS em passos de 0,5.
- Força = hMC (hybrid MMT8/CMAS, Varnier 2018), 0–100:
  - MMT8 unilateral, lado direito (o esquerdo se o direito não puder ser testado), 0–80
  - abdominais do CMAS: 6 manobras, 1 ponto cada (0–6)
  - elevação da cabeça do CMAS (0–5): 0 incapaz; 1 = 1–9 s; 2 = 10–29 s; 3 = 30–59 s; 4 = 60–119 s; 5 = ≥ 2 min
  - levantar do chão (ajoelhado → em pé), recodificado: 0, 2, 4, 6, 9
  - componente do JDMAI = teto((100 − hMC) / 10), ou seja, decis invertidos
- DAS pele = tipo (0–4) + distribuição (0–3) + 1 se houver QUALQUER sinal de vasculopatia + 1 se houver pápulas de Gottron de qualquer grau.
- Escala de Kendall 0–10 (manual IMACS): 0, T, 1–10. O traço (T) conta 0 na soma, porque o manual não lhe atribui número e o app oficial só aceita inteiros de 0 a 10.

## Pontos de corte (Wouters et al., RMD Open 2024)
| Estado | JDMAI1 | JDMAI2 |
|---|---|---|
| Doença inativa | ≤ 2,4 | ≤ 5,2 |
| Baixa atividade | 2,5–6,6 | 5,3–8,5 |
| Atividade moderada | 6,7–11 | 8,6–11,3 |
| Alta atividade | > 11 | > 11,3 |
Válidos apenas para pacientes sem acometimento gastrointestinal, cardíaco ou pulmonar.

## Decisões de conteúdo
- Ordem do exame = ordem preferida do IMACS: sentado (deltoide médio, bíceps, extensores do punho, quadríceps, dorsiflexores) → decúbito dorsal (flexores do pescoço, depois elevação da cabeça e abdominais do CMAS) → decúbito lateral sobre o lado esquerdo (glúteo médio) → decúbito ventral (glúteo máximo) → chão (levantar).
- O app oficial rotula o quadríceps como "hip flexion"; o teste correto é extensão do joelho.
- Tradução livre, sem validação transcultural. Manter esse aviso na página.
- Não guardar dados de pacientes (sem localStorage nem envio para servidor).

## Referências
- Rosina S et al. Rheumatology 2019;58:1196–205. doi:10.1093/rheumatology/key421
- Varnier GC et al. Arthritis Care Res 2018;70:1312–9. doi:10.1002/acr.23491
- Wouters C et al. RMD Open 2024;10:e003093. doi:10.1136/rmdopen-2023-003093
