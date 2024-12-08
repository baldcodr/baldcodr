---
title: "Building Multi-Agent AI System(MAS) on AWS"
datePublished: Sun Dec 08 2024 17:45:55 GMT+0000 (Coordinated Universal Time)
cuid: cm4fwa6yl00100ameb8mkdfrx
slug: building-multi-agent-ai-system-mas-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733676408726/df4b4535-6cca-4705-b4cb-9bfa36717def.webp
tags: ai, aws, amazon-bedrock, rag

---

### Why Multi-Agent Systems?

A single AI model may excel in specific tasks but struggle with multifaceted conversations. Multi-agent systems:

* Divide responsibilities (e.g., summarization, recommendations, or data extraction).
    
* Improve efficiency by delegating tasks to specialized agents.
    
* Provide modularity and scalability.
    

This article will explore how to build one of these MA systems using the recently released [multi-agent orchestrator](https://github.com/awslabs/multi-agent-orchestrator).

### Multi-Agent Orchestrator

The Multi-Agent Orchestrator is a flexible framework for managing multiple AI agents and handling complex conversations. It intelligently routes queries and maintains context across interactions. This makes it easy to interact with familiar AWS services and foundation models seamlessly.

### How it works?

The Multi-Agent Orchestrator comes with pre-built components that allow you to easily interact with Amazon Bedrock capabilities. The orchestrator is broken down into different components while providing a lot of flexibility in implementation.

### Implementation

We will be building **AgentFix**, an Incident Remediation System to help with the automated and prompt resolution of software issues without human intervention in the loop(self-healing).

### Core Components of our Orchestrator

#### Orchestrator

Functions as the primary coordinator for all other modules. Oversees the exchange of data between the Classifier, Agents, Storage, and Retrievers. Interprets user inputs and directs the creation of suitable responses. Manages errors and implements fallback procedures.

#### Classifier

Evaluates user queries, agent profiles, and previous conversation history. Selects the best-matched agent for each specific request. **Custom Classifiers**: Build entirely new classifiers for targeted tasks or specialized domains.

```python
# Initialize the orchestrator
custom_bedrock_classifier = BedrockClassifier(BedrockClassifierOptions(
    model_id='anthropic.claude-3-haiku-20240307-v1:0',
    client=bedrock_runtime_client,
    inference_config={
        'maxTokens': 500,
        'temperature': 0.7,
        'topP': 0.9
    }
))

# Initialize the orchestrator with some options
orchestrator = MultiAgentOrchestrator(options=OrchestratorConfig(
        LOG_AGENT_CHAT=True,
        LOG_CLASSIFIER_CHAT=True,
        LOG_CLASSIFIER_RAW_OUTPUT=True,
        LOG_CLASSIFIER_OUTPUT=True,
        LOG_EXECUTION_TIMES=True,
        MAX_RETRIES=3,
        USE_DEFAULT_AGENT_IF_NONE_IDENTIFIED=True,
        MAX_MESSAGE_PAIRS_PER_AGENT=10,
    ),
    classifier=custom_bedrock_classifier
    )
```

#### Agents

Prebuilt agents can be customized and enhanced to fit particular needs.

```python
from multi_agent_orchestrator.agents import (BedrockLLMAgent, BedrockLLMAgentOptions)
from multi_agent_orchestrator.agents import ChainAgent, ChainAgentOptions

def issue_classifier():
    agent = BedrockLLMAgent(BedrockLLMAgentOptions(
            name='Application Debugging Agent',
            description='Specializes in classifying application logs.',
            model_id='anthropic.claude-3-haiku-20240307-v1:0',
            streaming=True,
            inference_config={
                'maxTokens': 1000,
                'temperature': 0.7,
                'topP': 0.9,
            },
            custom_system_prompt={
            "template": """You are an expert in log analysis, able to categorize log data across multiple systems to allow easier issue resolution..
                Core Competencies:
                1. DevOps
                2. Software Architecture
                3. Metrics, Traces and Logging
                4. Application Monitoring
                5. Applciation Log Classifier

                When classifying logs, organise them with the following headings:
                - Issue:  
                - Root Cause:
                - Actions to be Taken:
                """
                    }
        ))

    return agent

def remediator():
    agent = BedrockLLMAgent(BedrockLLMAgentOptions(
            name='Application Remediator Agent',
            description='Specializes in providing remedition actions for debugging specific application error logs.',
            model_id='anthropic.claude-3-haiku-20240307-v1:0',
            streaming=True,
            inference_config={
                'maxTokens': 1000,
                'temperature': 0.7,
                'topP': 0.9,
            },
            custom_system_prompt={
            "template": """You are a site reliability engineer with expertise in  providing remedition actions and resolving complex application error from the application logs..
                Core Competencies:
                1. Programming Languages
                2. Software Architecture
                3. Best Practices
                4. Performance Optimization

                When providing resolution for issues:
                - Point out what the exact issue is
                - From the logs in the past 15 to 30 minutes find out the root cause
                - Explore actions to be taken to resolve the issue
                - Also include exact commands to run for each step in a linux environment if needed
                - Break down the resolution into actionable steps based on specific issue"""
                    }
        ))

    return agent

def chain_agent():
    agent = ChainAgent(ChainAgentOptions(
        name='FixerChainAgent',
        description='A simple chain of multiple agents',
        agents=[issue_classifier(), remediator()]
    ))
    
    return agent
```

#### Conversation Storage

Keeps a record of past interactions with in-memory storage. Operates on two distinct layers: context for the Classifier and context for the Agents.

#### Retrievers

Enhance the functionality of LLM-based agents by delivering relevant context and data. Optimize performance by retrieving needed information dynamically instead of relying entirely on pre-trained data. Retrieval can be from Bedrock Knowledge base or an entirely custom-built one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733677992469/fbf7c75b-95fc-4e50-994a-8e829b7d4386.png align="center")

### Steps:

1. We first need to set up our local environment to use [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html). For the required permissions, we can create roles [manually](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html) or with SSO. For larger teams managing multiple AWS Accounts with an Organisation, I recommend using [AWS TEAM](https://aws.amazon.com/blogs/security/temporary-elevated-access-management-with-iam-identity-center/) to manage access to your AWS environment.
    
    Once this is done, run the following commands to confirm that everything looks good:
    
    ```python
    # Show aws cli version
    aws --version
    
    # Get cli caller identity
    aws sts get-caller-identity
    ```
    
2. **Amazon Bedrock**: Access to foundation models from AWS partners. On the AWS console, you can request access to any of the models provided, we will be using the Anthropic Clause model `anthropic.claude-3-haiku-20240307-v1:0` for this demo.
    
3. To get started with AgentFix, follow these steps to install the required packages:
    
    1. Clone the repository:
        
        ```python
        git clone https://github.com/baldcodr/agentfix.git
        cd agentfix
        ```
        
    2. Create and activate a virtual environment (optional but recommended):
        
        ```python
        virtualenv -p python3.13 venv
        source venv/bin/activate  # On Windows use `venv\Scripts\activate`
        ```
        
    3. Install the required packages:
        
        ```python
        pip install -r requirements.txt
        ```
        

### Running Locally

To run the project locally, follow these steps:

1. Ensure that you have completed the installation steps above.
    
2. Run the application:
    
    ```python
    python main.py
    ```
    
3. Follow the prompts in the terminal to interact with the Multi-Agent system by inputting a sample log data as below.:
    
    ```python
    {"source": "app_log", "error_code": 500, "message": "Database timeout"}
    ```
    

### **Closing Remark**

Multi-agent systems are revolutionizing how we approach self-healing software solutions. By combining the autonomy, collaboration, and intelligence of MAS, organizations can achieve unparalleled system resilience and reliability.

**Call to Action:**

* Begin by implementing monitoring and anomaly detection with MAS concepts.
    
* Explore AWS tools to start building your self-healing architecture today!