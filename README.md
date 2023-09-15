<h1 align="center">Server NLW IA</h1>

O servidor da NLW SpaceTime foi desenvolvido durante o evento da Rocketseat no período dos dias 11 a 15 de setembro de 2023. A ideia da aplicação é focado na utilização da inteligência artificial da OpenAI, onde poderemos enviar um vídeo e pedir para a IA descrever algum prompt que pode ser um título ou uma descrição para um vídeo do Youtube.

<br/>

# 🚀 Tecnologias

Servidor desenvolvido com as seguintes tecnologias:

- Node JS
- TypeScript
- Fastify
- Prisma
- Prisma-Client
- SQLite
- OpenAI api
- zod

<br/>

# 👨‍💻 Uso da API da OpenAi no projeto

Uso na rota de criação de transcrição. Nesse processo, a IA irá criar um texto baseado em um áudio mp3 e no prompt enviado pelo usuário, sendo esse texto as palavras chaves citadas.

````typescript
const response = await openai.audio.transcriptions.create({
      file: audioReadStream,
      model: 'whisper-1',
      language: 'pt',
      response_format: 'json',
      temperature: 0,
      prompt
    })

````

Uso na rota da geração do texto por meio do modelo GPT 3.5, temperatura (define a criatividade da IA ao criar o texto) e as mensagens no prompt.O uso da stream nesse código é para dizer ao servidor que o texto será carregado aos poucos durante o processo de geração do texto. Isso será importante para podermos mostrar o texto em tempo real ao usuário e não somente quando o texto já estiver pronto. 

````typescript
const response = await openai.chat.completions.create({
      model: 'gpt-3.5-turbo-16k',
      temperature,
      messages:[
        { role: 'user', content: promptMessage}
      ],
      stream: true,
    })

````

