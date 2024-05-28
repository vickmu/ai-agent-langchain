# AI Email Assistant MVP

This project is a Minimum Viable Product (MVP) for an AI email assistant using LangChain, OpenAI, and external API integrations. The assistant can generate responses to emails, fetch weather data from an external API, and generate embeddings for email content.

## Project Structure

```
AI-AGENT-LANGCHAIN/
├── data/
│ ├── raw/
│ └── processed/
├── notebooks/
│ └── exploration.ipynb
├── src/
│ ├── init.py
│ ├── api/
│ │ ├── init.py
│ │ └── weather_api.py
│ ├── embeddings/
│ │ ├── init.py
│ │ └── embedder.py
│ ├── prompts/
│ │ ├── init.py
│ │ └── templates.py
│ └── main.py
├── tests/
│ ├── init.py
│ ├── test_api.py
│ ├── test_embeddings.py
│ └── test_prompts.py
├── .gitignore
├── README.md
├── pyproject.toml
└── poetry.lock
```

## Features

- **Prompt Templates**: Generate formatted prompts for email responses.
- **External API Calls**: Fetch weather data using the OpenWeatherMap API.
- **Embeddings**: Generate embeddings for email content using OpenAI embeddings.

## Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/vickmu/AI-AGENT-LANGCHAIN.git
    cd AI-AGENT-LANGCHAIN
    ```

2. **Install Poetry**:
    Follow the instructions to install Poetry from the [official documentation](https://python-poetry.org/docs/#installation).

3. **Install dependencies**:
    ```bash
    poetry install
    ```

4. **Activate the virtual environment**:
    ```bash
    poetry shell
    ```

## Configuration

- **API Keys**: Ensure you have the necessary API keys for OpenAI and OpenWeatherMap. You can set them as environment variables or directly in the code (not recommended for production).

## Usage

1. **Run the main script**:
    ```bash
    poetry run python src/main.py
    ```

2. **Example Code**:
    ```python
    from api.weather_api import get_weather
    from embeddings.embedder import generate_embedding
    from prompts.templates import get_formatted_prompt
    from langchain.llms import OpenAI
    from langchain.chains import LLMChain

    def main():
        email_text = "Dear Support, I am facing an issue with my order. Can you please help?"
        formatted_prompt = get_formatted_prompt(email_text)
        
        llm = OpenAI(api_key='your_openai_api_key')
        chain = LLMChain(llm=llm, prompt=formatted_prompt)
        response = chain.run(email=email_text)
        print("Generated Response:")
        print(response)
        
        city = "London"
        weather_info = get_weather(city)
        print(f"Weather Info for {city}:")
        print(weather_info)
        
        email_embedding = generate_embedding(email_text)
        print("Email Embedding:")
        print(email_embedding)

    if __name__ == "__main__":
        main()
    ```

## Project Modules

- **API**: Contains modules for making external API calls.
  - `weather_api.py`: Functions to fetch weather data from OpenWeatherMap.

- **Embeddings**: Modules for generating embeddings.
  - `embedder.py`: Code to generate embeddings using OpenAI.

- **Prompts**: Modules for handling prompt templates.
  - `templates.py`: Defines and formats prompt templates.

- **Main**: Entry point for the application.
  - `main.py`: Integrates all components and runs the application.

## Testing

1. **Run the tests**:
    ```bash
    poetry run pytest tests/
    ```

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss any changes.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
