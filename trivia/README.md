# Ultimate Trivia Assistant

A comprehensive AI-powered trivia assistant built with LangChain, AWS Bedrock, and Streamlit. This application provides multiple tools for trivia night management, including content generation, chat functionality with various memory types, and trivia simulation.

## Features

### 🎯 Core Tools
- **Promotion Maker**: Generate promotional content for trivia events
- **Report Writer**: Create detailed reports on any topic
- **Trivia Simulator**: Simulate trivia questions with contestant responses and judging
- **Chat Assistant**: Interactive chat with multiple memory configurations

### 🧠 Memory Types
- **Buffer Memory**: Stores entire conversation history
- **Window Memory**: Maintains a sliding window of recent interactions (5 exchanges)
- **Summary Memory**: Uses AI to summarize conversation history
- **DynamoDB Memory**: Persistent cloud-based conversation storage

## Architecture

The application uses:
- **AWS Bedrock** with Amazon Nova Lite v1.0 model for AI responses
- **LangChain** for chain orchestration and memory management
- **Streamlit** for the web interface
- **DynamoDB** for persistent chat storage
- **Boto3** for AWS service integration

## Prerequisites

- AWS Account with Bedrock access
- Python 3.8+
- AWS CLI configured with appropriate permissions
- Access to Amazon Nova Lite model in Bedrock

### Required AWS Permissions
- `bedrock:InvokeModel`
- `dynamodb:CreateTable`
- `dynamodb:DeleteTable`
- `dynamodb:PutItem`
- `dynamodb:GetItem`
- `dynamodb:Query`
- `dynamodb:Scan`

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd trivia
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Configure AWS credentials:
```bash
aws configure
```

4. Run the application:
```bash
streamlit run app.py
```

## Usage

### Web Interface
Access the application through your browser at `http://localhost:8501`

#### Promotion Maker
1. Select "Promotion Maker" from the sidebar
2. Enter theme, time, and location
3. Click "Submit" to generate promotional content

#### Report Writer
1. Select "Report Writer" from the sidebar
2. Enter a topic
3. Get an AI-generated report instantly

#### Trivia Simulator
1. Select "Trivia Simulator" from the sidebar
2. Enter a topic
3. View the generated question, two contestant responses, and host judgment

#### Chat Assistant
1. Select "Chat" from the sidebar
2. Choose memory type:
   - **Buffer**: Full conversation history
   - **Window**: Last 5 exchanges only
   - **Summary**: AI-summarized history
   - **DynamoDB**: Persistent cloud storage
3. For DynamoDB chat:
   - Click "Create Table" before first use
   - Click "Delete Table" to clean up

### Command Line Usage

Each module can be run independently:

```bash
# Promotion maker
python chains/promotion_maker.py

# Report writer
python chains/report_writer.py

# Trivia simulator
python chains/trivia_simulator.py

# Chat modules
python chains/buffer_chat.py
python chains/window_chat.py
python chains/summary_chat.py
python chains/dynamodb_chat.py
```

## File Structure

```
trivia/
├── app.py                          # Main Streamlit application
├── chains/                         # LangChain modules
│   ├── __init__.py                # Package initialization
│   ├── buffer_chat.py             # Buffer memory chat
│   ├── dynamodb_chat.py           # DynamoDB persistent chat
│   ├── promotion_maker.py         # Event promotion generator
│   ├── report_writer.py           # Topic report generator
│   ├── summary_chat.py            # Summary memory chat
│   ├── trivia_simulator.py        # Trivia game simulator
│   └── window_chat.py             # Window memory chat
├── images/
│   ├── bedrock_langchain.png      # Application logo
│   └── trivia assistant *.png     # Demo screenshots
├── requirements.txt               # Python dependencies
├── .gitignore                     # Git ignore rules
└── README.md                      # This file
```

## Technical Details

### LangChain Components Used
- **ChatBedrock**: AWS Bedrock chat model integration
- **PromptTemplate**: Template-based prompt construction
- **LLMChain**: Basic LLM chain execution
- **ConversationChain**: Conversation management
- **RunnableParallel**: Parallel chain execution
- **Memory Classes**: Various conversation memory implementations

### Memory Implementations
- **ConversationBufferMemory**: Stores all messages
- **ConversationBufferWindowMemory**: Sliding window (k=5)
- **ConversationSummaryMemory**: AI-powered summarization
- **DynamoDBChatMessageHistory**: Cloud persistence

### Model Configuration
- **Model**: amazon.nova-lite-v1:0
- **Max Tokens**: 200-300 (varies by use case)
- **Temperature**: 0.5 (for trivia simulator)
- **Stop Sequences**: ["User", "human"] to prevent self-continuation

## Troubleshooting

### Common Issues

1. **AWS Credentials**: Ensure AWS CLI is configured with valid credentials
2. **Bedrock Access**: Verify access to Amazon Nova Lite model in your region
3. **DynamoDB Permissions**: Check IAM permissions for DynamoDB operations
4. **Model Availability**: Ensure Nova Lite is available in your AWS region

### Error Messages
- `SyntaxError`: Check Python syntax in modified files
- `AccessDenied`: Verify AWS permissions
- `ModelNotFound`: Confirm model availability in your region

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source and available under the MIT License.

## Support

For issues and questions:
1. Check the troubleshooting section
2. Review AWS Bedrock documentation
3. Consult LangChain documentation
4. Open an issue in the repository

## Demo Screenshots

### Main Interface
![Main Interface](./images/trivia%20assistant%201.png)

### Promotion Maker
![Promotion Maker](./images/trivia%20assistant%202.png)

### Report Writer
![Report Writer](./images/trivia%20assistant%204.png)
![Report Writer](./images/trivia%20assistant%205.png)

### Trivia Simulator
![Trivia Simulator](./images/trivia%20assistant%206.png)


### Chat Interface - DynamoDB Memory
![Chat DynamoDB Memory](./images/dynamodb.png)

### DynamoDB Session Table
![DynamoDB Session Table](./images/trivia%20assistant%20session%20table.png)

---

Built with ❤️ using AWS Bedrock, LangChain, and Streamlit

## License

This repository contains my original code and documentation developed as part of the
AWS Cloud Institute curriculum. All portions authored by me are licensed under the
[MIT License](./LICENSE).

**Important Note:** AWS-provided lab materials (including starter code, lab instructions,
and proprietary content) remain the intellectual property of Amazon Web Services, Inc.
and are not covered under this license.