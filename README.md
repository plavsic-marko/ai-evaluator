# AI Evaluator

AI Evaluator je softverski sistem za strukturiranu, fer i preciznu evaluaciju performansi AI agenata (chatbotova) na osnovu njihovih odgovora i usklađenosti sa definisanim system promptom.

## Pregled projekta

Projekat je podeljen u tri nezavisna modula, svaki sa jasno definisanom ulogom:

1. **Generator kriterijuma** - Analizira system prompt AI agenta i generiše kriterijume za evaluaciju:
   - Standardni kriterijumi (fiksni, skala 0-10)
   - Dinamički kriterijumi (specifični za prompt, skala 0-1 ili 0-10)

2. **Generator pitanja** - Kreira set od 20 relevantnih pitanja koja testiraju znanje i sposobnosti AI agenta u njegovom domenu.

3. **Evaluator odgovora** - Procenjuje odgovore AI agenta prema generisanim kriterijumima i daje strukturirane rezultate evaluacije.

## Funkcionalnosti

- **Dinamičko generisanje kriterijuma** - Prilagođeni kriterijumi za različite tipove agenata
- **Fleksibilne skale ocenjivanja** - 0-10 za kvalitativne procene, 0-1 za binarne kriterijume
- **Sistematsko generisanje test pitanja** - Fokusirana na relevantnost i raznovrsnost
- **Strukturirana evaluacija** - Jasno definisani XML tagovi i format izlaza
- **JSON format rezultata** - Lak za dalju obradu i analizu

## Instalacija

### Preduslovi

- Python 3.8+
- Anthropic API ključ

### Koraci

1. Klonirajte repozitorijum:
```bash
git clone https://github.com/plavsic-marko/ai-evaluator.git
cd ai-evaluator
```

2. Instalirajte potrebne biblioteke:
```bash
pip install anthropic
```

3. Podesite Anthropic API ključ kao environment varijablu:
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

## Upotreba

### Primer u Jupyter Notebook-u

Projekat je organizovan u ćelije koje se mogu pokrenuti u Jupyter Notebook-u:

#### Ćelija 0: Importi i API postavke
```python
import os
from anthropic import Anthropic

# Postavke Anthropic API-ja
anthropic_client = Anthropic(
    api_key=os.environ.get("ANTHROPIC_API_KEY")
)

# Definicija osnovnih konstanti
CLAUDE_MODEL = "claude-3-5-sonnet-20240620"
MAX_TOKENS = 4096
```

#### Ćelija 1: Generator kriterijuma
```python
def extract_elements(text, tag_name):
    """
    Izvlači sadržaj iz XML taga.
    """
    import re
    
    pattern = f"<{tag_name}>(.*?)</{tag_name}>"
    matches = re.findall(pattern, text, re.DOTALL)
    
    return matches

# Definicija standardnih kriterijuma
STANDARD_CRITERIA = """
Below are the standard evaluation criteria you must assess in every evaluation:
- Relevance (0–10): Response directly addresses the user's query and is on-topic.
- Accuracy (0–10): Information provided is factually correct and up-to-date.
...
"""

def generate_criteria(agent_system_prompt):
    """
    Generiše dinamičke kriterijume evaluacije na osnovu system prompta AI agenta.
    """
    # Implementacija funkcije
```

#### Ćelija 2: Generator pitanja
```python
def generate_questions(agent_system_prompt):
    """
    Generiše set od 20 test pitanja na osnovu system prompta AI agenta.
    """
    # Implementacija funkcije
```

#### Ćelija 3: Evaluator odgovora
```python
def evaluate_response(agent_description, agent_system_prompt, original_task, agent_response, combined_criteria):
    """
    Evaluira odgovor AI agenta na osnovu standardnih i dinamičkih kriterijuma.
    """
    # Implementacija funkcije

def extract_criteria_scores(evaluation_text):
    """
    Izvlači ocene za svaki kriterijum iz teksta evaluacije.
    """
    # Implementacija funkcije

def run_full_evaluation(agent_description, agent_system_prompt, original_task, agent_response):
    """
    Izvršava kompletan proces evaluacije agenta.
    """
    # Implementacija funkcije
```

#### Ćelija 4: Primer evaluacije
```python
# Primeri agenata za testiranje
NUTRITIONIST_DESCRIPTION = "AI asistent za pružanje informacija o zdravoj ishrani"
NUTRITIONIST_PROMPT = """
Ti si stručni nutricionista koji daje savete o zdravoj ishrani.
...
"""

# Funkcija za pokretanje evaluacije i prikaz rezultata
def evaluate_and_show_results(agent_description, agent_system_prompt, original_task, agent_response):
    # Implementacija funkcije

# Pokretanje interaktivne evaluacije
if __name__ == "__main__":
    # Kod za izbor primera i pokretanje evaluacije
```

### Pokretanje kompletne evaluacije

```python
results = run_full_evaluation(
    agent_description="Opis AI agenta",
    agent_system_prompt="System prompt za AI agenta",
    original_task="Pitanje za AI agenta",
    agent_response="Odgovor AI agenta na pitanje"
)

print(results["evaluation_json"])
```

## Struktura kriterijuma

### Standardni kriterijumi (skala 0-10)
- Relevance - relevantnost odgovora
- Accuracy - tačnost informacija
- Coherence - logička struktura
- Conciseness - sažetost
- Clarity - jasnoća
- Completeness - potpunost
- Language Appropriateness - prikladnost jezika
- Chain-of-Thought Reasoning - logičko rasuđivanje korak po korak

### Dinamički kriterijumi (skala 0-1 ili 0-10)
- Specifični za svaki system prompt
- Generisani automatski na osnovu analize prompta
- Mogu biti binarni (0-1) ili kvalitativni (0-10) u zavisnosti od prirode kriterijuma

## Primeri agenata za testiranje

Sistem uključuje tri predefinisana primera za testiranje:

1. **Nutricionistički asistent** - daje savete o zdravoj ishrani
2. **Sportski asistent** - odgovara na pitanja o srpskim NBA igračima
3. **Zdravstveni asistent** - pruža informacije o zdravlju, ishrani i fizičkoj aktivnosti

## Izlaz evaluacije

Rezultati evaluacije su dostupni u JSON formatu koji sadrži:

```json
{
  "criteria": {
    "Criterion Name 1": {
      "justification": "Obrazloženje ocene",
      "score": 8.5
    },
    "Criterion Name 2": {
      "justification": "Obrazloženje ocene",
      "score": 1
    },
    ...
  },
  "overall": {
    "justification": "Ukupno obrazloženje",
    "score": 8.2
  }
}
```

## Buduća poboljšanja

- Vizualizacija rezultata (grafikoni)
- Agregacija kroz vreme (praćenje performansi)
- Uporedna analiza više agenata
- Automatizacija testiranja

## Licenca

MIT