# POC 6 - Aplicação NextJS: Sistema de Reservas de Assentos

Este é um projeto desenvolvido em Next.js com foco na criação de uma interface para reserva de assentos de cinema. O projeto apresenta uma página responsiva com suporte a temas Light e Dark, utilizando dados de um arquivo JSON.

## Objetivo:

Criar uma interface interativa e responsiva que permita:

- Selecionar assentos disponíveis.
- Exibir informações sobre o filme e o cinema.
- Realizar a compra dos ingressos com cálculo do valor total.


## Tecnologias Utilizadas: 
- Next.js 14+
- React 18+
- HTML5 e CSS3 (Flexbox)
- Media Queries para responsividade e temas
- JSON para simular dados dinâmicos

## Planejamento Visual: 
Temas que estaram nesse projeto: 

-  Light/Dark Mode

![corespoc6](https://github.com/user-attachments/assets/67809e2a-3c3d-4748-a3ea-dda1f0b5ed40)


## Passo a Passo para Criar o Projeto: 
1. Instalar o Node.js e npm
Certifique-se de ter o Node.js (versão 18 ou superior) instalado no seu computador.
Para verificar, execute os comandos:

```
node -v
npm -v
```

2. Criar o Projeto Next.js:
- Abra o prompt de comando (para isso aperte windowns + R em seguida digite cmd)
- Ou  o terminal do vscode (para isso vá até vs code e aperte Ctrl + a tecla debaixo do Esc, isso varia dependendo do seu teclado)
- E execute o seguinte comando:

```
npx create-next-app@latest poc6
```
3. Durante a criação, você pode personalizar algumas opções (ou deixar as configurações padrão):

- Siga conforem a imagem abaixo:

![poc8](https://github.com/user-attachments/assets/cef1cfb1-42d3-4719-960d-d987bc7caf99)

4. Acesse a pasta do projeto:

```
cd poc6
```

5. Instalar Dependências
- No diretório do projeto, execute:
```
npm install
```
Isso garantirá que todas as dependências básicas do Next.js sejam instaladas.

6. Inicie o servidor de desenvolvimento

```
npm run dev
```
A aplicação estará disponível em `http://localhost:3000.`

## Estrutura do Projeto: 

POC6/
├── src/
│   ├── components/
│   │   └── Seat.jsx
│   │   └── seat.module.css
│   ├── data/
│   │   └── dados.json
│   ├── styles/
│   │   └── globals.css
│   │   └── page.module.css
│   └── pages/
│       └── index.js
├── package.json
├── README.md


## Adicionar Dados dos Assentos: 
- No arquivo `src/data/dados.json` coloque: 

 
```
{
  "titulo": "Todo tempo que temos",
  "sinopse": "Almut e Tobias são unidos por um encontro surpresa...",
  "direcao": "John Crowley",
  "horario": "19:30",
  "data": 10 de novembro de 2024,
  "assentos": [
    { "numero": 1, "disponivel": false }, 
    { "numero": 2, "disponivel": true },
    ...
  ]
}


```

## Criar o Componente de Assento
- No arquivo `src/components/Seat.jsx` coloque:

```

import styles from "./seat.module.css";

export default function Seat({ numero, disponivel, onClick, selected, purchased }) {
  return (
    <div
      className={`${styles.seat} ${
        disponivel ? styles.available : styles.unavailable
      } ${selected ? styles.selected : ""} ${purchased ? styles.purchased : ""}`} 
      onClick={() => disponivel && !purchased && onClick(numero)} 
    >
    </div>
  );
}

```

## Estilizar o Projeto: 
-  Light/Dark Mode
- No arquivo `src/styles/globals.css` coloque:

```
:root {
  --background-color: #F0F0F0;
  --foreground-color: #1A1A24;
  --primary-color: #D83D2E;
  --secondary-color: #505050;
  --text-color: #000000;
  --available: #BABABA;
  --unavailable: #1A1A24;
}
}

```
- Esse código é responsável pela definição da paleta de cores no light mode.
![poc7](https://github.com/user-attachments/assets/1b4b946e-e674-4bb4-8a98-3a39946d2931)

```

@media (prefers-color-scheme: dark) {
  :root {
    --background-color: #1A1A24;
    --foreground-color: #F0F0F0;
    --primary-color: #D83D2E;
    --secondary-color: #BABABA;
    --button-text: #F0F0F0;
    --available: #F0F0F0;
    --unavailable: #505050;
  }
}
```

-  Com o uso do @media (prefers-color-scheme: dark), definimos as cores do dark mode, caso seja essa a preferência do usuário.

 ![poc9](https://github.com/user-attachments/assets/ad428a2b-7179-4ee1-9d6f-f1ee8073b307)

```

  body {
  background-color: var(--background-color); 
  color: var(--foreground-color);                 
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  transition: background-color 0.3s ease, color 0.3s ease; 
}

```
- Esse é o código de configuração geral do comportamento de body.

## Organização dos assentos: 
- No arquivo `src/styles/page.module.css` colouque:

```
  margin-bottom: 20px;
}

.seatingChart {
  display: grid; grid-template-columns: repeat(8, 1fr); gap: 10px;margin-top: 20px;
}

.buyButton {
  margin-top: 20px; padding: 10px; background-color: var(--primary-color);color: white;border: none;border-radius: 5px;cursor: pointer;
}
.extraRow {
  grid-template-columns: repeat(4, 1fr); margin-top: 10px;  display:flex;  justify-content: space-around;  
}

.tela {
  width: 100%;height: 20px;background-color: var(--available);border-radius: 10px;margin: 20px auto;text-align: center;line-height: 20px;font-size: 14px;font-weight: bold;
}

.legenda {
  display: flex;justify-content: center;gap: 20px;margin-top: 20px;
}

.legendaItem {
  display: flex;align-items: center;gap: 8px;
}

.legendaCirculo {
  width: 15px; height: 15px; border-radius: 50%;
}

```
- Isso definira os estilos para organizar e estilizar elementos de uma aplicação de reservas de assentos

## Responsividade
- Layout adaptado para dispositivos móveis, tablets e desktops usando Media Queries.
- Temas Light e Dark podem ser alternados com base nas preferências do sistema operacional ou configurados manualmente.

1.1.  Adaptação Geral do Layout Flexibilidade do container principal (.container):
- Para telas menores, o layout muda de "row-reverse" (elementos alinhados lado a lado) para uma disposição em coluna. Isso é feito usando: No arquivo `src/styles/page.module.css`:

```

@media (max-width: 768px) {
  .container {
    flex-direction: column;
    gap: 20px;
    padding: 10px;
  }
}

```

- A largura máxima do container é ajustada dinamicamente com max-width, garantindo que ele se adapte a telas pequenas e grandes. 5.2. Ocultação de Informações em Telas Menores Em telas menores que 768px, apenas o título e o horário do filme permanecem visíveis:

 ```

@media (max-width: 768px) {
  .movieInfo p, 
  .movieInfo h3 {
    display: none; /* Oculta a sinopse e subtítulos */
  }
}

```

- O título é centralizado para melhorar a legibilidade:

```
@media (max-width: 768px) {
 .movieInfo h2 {
   text-align: center;
 }
}

```

1.2. Organização da Grade de Assentos A grade de assentos (.seatingChart) foi configurada para se ajustar ao tamanho da tela: Desktop: 8 colunas são exibidas, aproveitando o espaço.


```
.seatingChart {
  grid-template-columns: repeat(8, 1fr);
}

```

- Telas menores (480px): O espaçamento entre os assentos (gap) foi reduzido. Margens ajustadas para acomodar melhor os assentos:

```
@media (max-width: 480px) {
  .seatingChart {
    gap: 2px;
    margin-right: 2px;
    margin-top: 0;
  }
}

```

1.3. Botão de Compra Para telas pequenas, o botão de compra foi ajustado: Margens e alinhamento centralizado:

```
@media (max-width: 768px) {
  .buySection {
    margin-left: 0;
    margin-top: 15px;
    margin-bottom: 30px;
  }
}

```

- Para telas muito pequenas (480px), a altura do botão foi aumentada para melhorar a usabilidade:

```


@media (max-width: 480px) {
  .buyButton {
    height: 70px;
  }
}

```

1.4. Componente extraRow Representando uma fileira extra de assentos, o componente foi configurado para manter espaçamento e centralização: Em telas menores, ajustes garantem que ele continue alinhado:


```

@media (max-width: 480px) {
  .extraRow {
    gap: 10px;
    margin-right: 2px;
    margin-top: 2px;
  }
}

```

1.5. Outros Ajustes Importantes Tela do cinema (.tela) 
-  Outros Ajustes Importantes Tela do cinema (.tela):
-  Redução de fonte para dispositivos menores:

```

@media (max-width: 768px) {
  .tela {
    font-size: 12px;
  }
}

```

- Resultado: essas configurações garantem que o projeto funcione de maneira fluida em qualquer dispositivo. Em telas menores, a interface prioriza a clareza e a usabilidade, ocultando informações secundárias (como sinopse) e ajustando elementos como grades e botões para que fiquem acessíveis e visualmente organizados.

### Importação de Dependências: 

```

**import { useState, useEffect } from "react";
import data from "./data/dados.json";
import Seat from "./components/Seat";
import styles from "./styles/page.module.css";**

```
- useState: Para gerenciar o estado local dos assentos selecionados.
- useEffect: Para sincronizar os assentos comprados com o `localStorage`.
- data: Carrega os dados do filme e dos assentos a partir de um arquivo JSON.
- Seat: Importa o componente Seat, que representa cada assento individual.
- styles: Importa os estilos CSS para a página principal.

### Gerenciamento de Estado:

```

const [selectedSeats, setSelectedSeats] = useState([]);

```
- O estado selectedSeats armazena os números dos assentos que foram selecionados pelo usuário.

### Função para Gerenciar a Seleção de Assentos

```

const OrganizarSelectSeat = (numero) => {
  setSelectedSeats((prev) =>
    prev.includes(numero)
      ? prev.filter((n) => n !== numero)
      : [...prev, numero]
  );
};

```
- Isso faz com que altere a seleção dos assentos. Se o número do assento já estiver na lista (selectedSeats), ele será removido. Caso contrário, será adicionado. Essa lógica permite que o estado se atualize dinamicamente à medida que o usuário interage com os assentos.

### Cálculo do Total:

```

const total = selectedSeats.length * ticketPrice;

```
- Multiplica o número de assentos selecionados pelo preço fixo de cada ingresso (ticketPrice).

### Estrutura do Componente: 

```

return (
  <main className={styles.container}>
    <div className={styles.movieInfo}>
      <h2>{data.titulo}</h2>
      <p>{data.sinopse}</p>
    </div>
    <div className={styles.seatingChart}>
      {data.assentos.map((seat) => (
        <Seat
          key={seat.numero}
          {...seat}
          onClick={OrganizarSelectSeat}
          selected={selectedSeats.includes(seat.numero)}
        />
      ))}
    </div>
    <button className={styles.buyButton}>
      Comprar ({selectedSeats.length}) - R$ {total.toFixed(2)}
    </button>
  </main>
);

```
- Mostra o título e a sinopse extraídos do JSON.
- Grade de Assentos: Usa `data.assentos.map()` para renderizar dinamicamente os assentos.
- Botão de Compra: Exibe a quantidade de assentos selecionados e o preço total calculado. Exemplo se o preço do ingresso for R$25,00:

![poc20](https://github.com/user-attachments/assets/03fac270-a977-4ac7-971b-e397074b2f53)

## como usar a aplicação após configurada: 

1. Abra a aplicação no navegador em `http://localhost:3000`.
2. Escolha os assentos disponíveis clicando sobre eles.
3. Clique no botão "Comprar" para finalizar e veja o total no alerta de confirmação.


  
