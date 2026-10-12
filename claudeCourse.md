Models:
Opus: higth intelligence, high cost and latency
sonne: balance, intelligence, cost, spped
haiku: cost/speed effectice

system prompts: Esto es sobre tener un aestructura de promts de forma que las respyestas
esten mejor pensadas, darle un role a claude, decirle que como queremos la respuesta, o que fuentes tomar para docuemnetarse

temperature: esto es sobre que tan creativas son las respuest de claude (0-1)

streaming: podemos usar este feature para obtener respuestas por chunks y hacer visualizar la respuesta progresivamente

grader
code
model
human

prompt engeeniring

- be clear and direct
- being especific:
  - provide guidelines
    - Prefer simple solutions over complex abstractions
    - Reuse existing patterns in the codebase
    - Do not introduce new dependencies unless necessary
    - Keep changes small and focused
    - Consider backward compatibility
    - Prioritize maintainability over cleverness
  - provide steps
    - Troubleshooting hard problems
    - decicion making
    - critical thinking
    - anytime you want claude to force a consider a "wide" view
  - structure with XML tags
    - we can use XML tags to wrap up code or documentation, so the model can understand better the prompt
  * multi shot prompting example
    - we can provide diferent kinds of examples or scenarios, so the model can understand better how to responde to the promt

RAG (Retrieval augmented generation) and AGENTIC SEARCH

- text chunking strategies
  - size based chinking
  * structure based chunking
    - semantic based chuncking
    * sentence based chunking

- semantic search embeddings
  - primero dividimos el texto en chunks
  * luego usamos text embedding para convertir cada chunk en un vector de numeros
  * guardamos los text embeddings en una base de datos de vectores
  * luego aplicamos text embeddings en la pregunta que esta haciendo el usuario
  * luego asplicamos cosine similarity
  * luego sabiendo que vectores tienen la mayor similitud buscamos los chunks correspondientes
  * y podemos mandarle esos chunck al prompt junto a nuestra pregunta y asi obtener un buen resultado.
- Lexical search
  - aplicamos BM25
    - tokenize the query
    - count term frequency (la idea es ver cuantas veces se repite cada palabra en cada chunck)
    * weigth terms by importance (La palabra que menos se repite a travez de los chunks tiene mayor peso al decidir que chunks tienen lo que buscamos)
    * find best maches
  * merge index aproaches

FEATURES OF CLAUDE

- Extended thinking: podemos aumentar este parametro cuando no tenemos un prompt bien construido, entonces claude usar una cantidad de tokens para razonar sobre el prompt y mejorar los resultados.

* Images support: podemos enviar imagenes a claude, mandarle examples de lo que le pediomos. Un buen prompt ayudara a claude a hacer un mejor trabajo
* suport pdf: puede extraer y entender el contenido, tablas, graficos... un buen prompt ayuda
* citations: POdemos habilitar este feature cuando queremos validar la fuente de informacion

CLAUDE CODE AND COMPUTER USE

- Effort multiplier
  - Feed context into Claude
  - tell claude to plan a solution
  - ask claude to implement a solution

* test driven development for better results
  - feed context into claude
  * ask clade to think of test cases
  - ask claude to implement those test cases
  - ask claude to write code that passes the test cases\

  Comands
  - /clear => clear conversation history and resets context
  * /init => scans codebase and creates CLAUDE.md doc, podemos usarlo para actualizar el CLUADE.md file
  * # - Adds notes to your claude.md

mcps

- figma
- playwright
- firecrawler
- slack
- JIRA
- gitHub

AGENTS and WORKFLOWS

- WORKFLOWS
  - parallelization workflow
    - Use this workflow when an AI feature is complex enough to be split into several independent sub-tasks, where none depends on another's output.
    - Workflow type
      - Split a single task into multiple sub-tasks
      - Run the sub-tasks in parallel
      - Aggregate the results together
      - The parallelized sub-tasks don't need to be identical: each can have its own specialized prompt, set of tools, etc.
  - chaining workflow
    Chaining workflows work well when:
    - Your task can be broken down into a fixed sequence of clear, distinct steps
    - Each step produces an output that the next step needs as its input
    - A single prompt struggles to do everything well at once (long, multi-part instructions)
    - The gain in accuracy and reliability outweighs the extra latency and cost of making several calls
      This pattern is especially valuable for content pipelines (outline, then draft, then edit), generate-then-translate or generate-then-review tasks, and any application where you want to check or validate an intermediate result before moving on to the next step.
  - routing workflow
    Routing workflows work well when:
    - Your application handles diverse types of requests that need different approaches
    - You can clearly define categories that cover your use cases
    - The categorization step can be handled reliably by Claude
    - The performance benefit of specialized processing outweighs the overhead of the routing ste
      This pattern is especially valuable for customer service bots, content generation tools, and any application where the "right" response depends heavily on understanding the type of request being made.

- AGENTS
  Agents work well when:
  - You can't predict in advance the exact steps needed to complete the task
  - The task is open-ended: the path depends on what Claude discovers along the way
  - You can give Claude a clear goal and a set of tools, and let it decide which to use and in what order
  - Claude can check its own progress by observing the results of its actions (tool results, test output, the state of the environment)
  - The flexibility outweighs the higher cost, latency, and unpredictability compared to a workflow
    This pattern is especially valuable for coding assistants, research tasks, and any application where users can ask for many different things that you can't map to a predefined sequence of steps.
  - Agents vs workflows
    - Workflow: you define the steps, Claude executes each one
    - Agent: you define the goal and the tools, Claude plans the steps itself
    - Workflows are more predictable and easier to test, so prefer a workflow whenever the steps are known, and use an agent only when you need the flexibility
