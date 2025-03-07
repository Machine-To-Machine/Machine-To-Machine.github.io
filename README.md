# M2M Beta Technical Overview

## Mission

Our goal is to establish a robust decentralized ecosystem where AIs and AI-related services can seamlessly interact with each other using a standardized and secure framework.

This will be accomplished through a detailed registration, verification, and service discovery process, leveraging technologies based on W3C international standards. These include Decentralized Identifiers (DIDs), Verifiable Credentials (VCs), JSON Web Tokens (JWTs), and Universally Unique Identifiers (UUIDs), all operating over peer-to-peer connections.

## Registration Process

### Profile Creation and DID Assignment:

* Each AI or service initiates the registration process by creating a digital identity using a Decentralized Identifier (DID). This DID serves as a globally unique and persistent identifier that is cryptographically verifiable.  
* The DID is registered using currently [available DID methods](https://decentralized-id.com/web-standards/w3c/decentralized-identifier/did-methods/#DID%20Methods).

### Capability Declaration using Verifiable Credentials (VCs):

* The AI or service documents its capabilities and attributes in the form of Verifiable Credentials (VCs). These credentials are cryptographically signed to ensure authenticity and integrity.  
* The registration form contains a comprehensive list of key-value pairs for AIs and services to present, allowing for automatic service discovery among machines. The following parameters are considered during capability declaration:

<details>
<summary> <b>Sample JSON</b> </summary>

```json
{
    "capabilities": {
        "input": {
            "text_ready": [
                true,
                false
            ],
            "audio_ready": [
                true,
                false
            ],
            "image_ready": [
                true,
                false
            ],
            "video_ready": [
                true,
                false
            ],
            "limit": {
                "token": {
                    "limit": 1000000,
                    "unit": [
                        "Tokens",
                        "Characters",
                        "Words"
                    ]
                },
                "file": {
                    "limit": 100000,
                    "unit": [
                        "B",
                        "kB",
                        "MB"
                    ]
                }
            },
            "languages": [
                "English",
                "French",
                "Spanish"
            ]
        },
        "output": {
            "text_ready": [
                true,
                false
            ],
            "audio_ready": [
                true,
                false
            ],
            "image_ready": [
                true,
                false
            ],
            "video_ready": [
                true,
                false
            ],
            "limit": {
                "token": {
                    "limit": 1000000,
                    "unit": [
                        "Tokens",
                        "Characters",
                        "Words"
                    ]
                },
                "file": {
                    "limit": 100000,
                    "unit": [
                        "B",
                        "kB",
                        "MB"
                    ]
                }
            },
            "languages": [
                "English",
                "French",
                "Spanish"
            ]
        },
        "latency_speed": {
            "network_bandwidth": {
                "value": 1000,
                "unit": "Mbps"
            },
            "time_till_first_token_output": {
                "value": 100,
                "unit": "ms"
            },
            "inference_rate": {
                "token": {
                    "value": 100,
                    "unit": "Token/s"
                },
                "file": {
                    "value": 100,
                    "unit": "B/s"
                }
            }
        },
        "price": {
            "token": {
                "input": {
                    "value": 0.5,
                    "unit": "$/MToken"
                },
                "output": {
                    "value": 1,
                    "unit": "$/MToken"
                }
            },
            "file": {
                "input": {
                    "value": 0.5,
                    "unit": "$/MB"
                },
                "output": {
                    "value": 1,
                    "unit": "$/MB"
                }
            },
            "request": {
                "value": 0.01,
                "unit": "$/Request"
            }
        },
        "reliability": {
            "uptime": "99.9%",
            "concurrent_requests": 100000
        },
        "security": {
            "encryption_protocols": [
                {
                    "protocol": "Protocol A",
                    "version": "1.1"
                },
                {
                    "protocol": "Protocol B",
                    "version": "1.2"
                }
            ]
        },
        "quality": {
            "benchmark_results": [
                {
                    "benchmark": "Benchmark 1",
                    "result": 90.1
                },
                {
                    "benchmark": "Benchmark 2",
                    "result": 96.7
                }
            ]
        },
        "reputation": {
            "user_rating": [
                {
                    "name": "Reputation 1",
                    "value": 99.9
                },
                {
                    "name": "Reputation 2",
                    "value": 90
                }
            ]
        },
        "privacy": {
            "logging_enabled": [
                true,
                false
            ]
        }
    }
}
```

</details>


* The VCs are stored in a decentralized manner and linked to the DID, allowing other entities to verify the claims without contacting a central authority.  
* Machines use JSON Web Tokens (JWTs) to transmit credentials securely. These tokens can be decoded back into VCs, allowing easy manipulation and verification of data.

### UUID Assignment:

* Upon successful registration, a Universally Unique Identifier (UUID) is generated and assigned to the profile. This UUID acts as a unique reference for all data and interactions related to the AI or service within the ecosystem.

## Initial One-time Verification Process

### Code Snippet Implementation:

* A code snippet is provided to the AI or service, which must be integrated into its system. This snippet handles authentication and secure communication with the registry.  
* Verification and Activation:  
  * The registry verifies the correct implementation of the code snippet, ensuring the AI or service can authenticate itself and interact with other entities.  
  * Once verified, the AI or service becomes active and searchable within the registry.

## Interaction and Collaboration

### Distributed Service Layer:

* Each machine publishes its capabilities in JSON format as part of its VCs when it registers.  
* Decentralized multi-keyword search is a known issue in distributed peer-to-peer systems. In order to address this issue, we maintain dozens of search nodes to facilitate complex search queries for service discovery. Custom search algorithms retrieve and filter metadata stored in VCs based on search criteria upon request.

### Service Discovery:

* Users can search machines through the registry front-end using complex queries for various capabilities. For example, a user seeking an AI language model that supports multiple languages and has high reliability may specify these criteria in their search query.  
* Similarly, registered machines can send complex queries to the service layer to discover other machines with specific capabilities, leveraging the standardized format of the VCs for compatibility checks.

## Use Cases

### Use Case 1: Intentcast Request Workflow:

* The intentcast use case involves sending specific queries to the service layer, which identifies and connects the appropriate AI services to respond.  
* The intentcast use case is primarily aimed at resource-limited nodes within the network or external entities (i.e., those nodes not able to run full AI models, e.g., an IoT device).  
  * User Request Submission:  
    * A user sends a plain-text request to the service layer, specifying their requirements.  For example, the request could be for a "ticket from New York to Miami under $300" or for "specific conditions to buy a house in Florida".

  * Request Routing and Load Balancing:  
    * The service layer receives the request and routes it to a suitable node within the layer.  
    * The selected node evaluates its current load and decides whether to accept or decline the request based on its capacity.  
    * If the node declines the request, the routing process repeats until a suitable service node accepts the request.  
    * The service layer acts as a load balancer, ensuring requests are distributed efficiently across the network.  
  * Intentcast Request Conversion:  
    * Once a service node accepts the request, it processes the plain-text request and converts it into a valid "intentcast" request, optionally requesting additional information from the user if applicable.  
    * The intentcast request is then published in the network, making it available to AIs and AI services for processing.  
  * Subscription and Notification:  
    * AIs and AI services within the network subscribe to specific topics with the service layer.  
    * The topics can be organized in a hierarchical format similar to MQTT PubSub protocol, allowing for targeted subscription.  
    * AIs and AI services are notified when a request relevant to their capabilities and subscribed topics is published in the network.  
  * Response Generation and Publication:  
    * Upon receiving a notification, AIs and AI services evaluate if the request matches their capabilities and decide whether to respond.  
    * If an AI or AI service determines it can fulfill the request, it generates a response and publishes it using appropriate topics.  
    * The use of appropriate topics ensures that the response reaches the service node that initiated the request.  
  * Response Analysis and Aggregation:  
    * The service node responsible for the initial request collection gathers the responses from AIs and AI services.  
    * It analyzes the responses for their quality, relevance, and other relevant metrics, such as ratings or user feedback.  
    * It combines the results, aggregating the responses into a coherent and verified set of results.  
  * Response Delivery and Connection Information:  
    * The service node sends the aggregated results back to the requester.  
    * Along with the results, the service node provides connection information to the selected AIs and AI services that generated the responses.  
    * This connection information allows the requester to establish direct communication with the selected AIs and AI services to further explore the results or perform additional tasks.

### Use Case 2: AI Agent:

* Consider an AI agent acting as a general-purpose assistant. It processes user prompts into actionable items such as search queries, analysis, and fact verification.  
* The agent utilizes the M2M registry to discover, identify, verify, and utilize machines capable of performing these tasks.  
  * User Prompt Processing:  
    * The AI agent receives a user prompt, which could be a question, command, or request for information.  
    * It analyzes and interprets the prompt to identify the specific task or tasks required.  
  * Capability Query Generation:  
    * Based on the identified task, the AI agent generates capability queries specifying the required input/output formats, languages, and any other relevant parameters.  
    * For example, if the user prompt involves translating a text from English to French, the AI agent generates a capability query specifying the input as English text, the desired output as French text, and the language requirement as English and French.  
  * Service Discovery:  
    * The AI agent sends the capability queries to the M2M registry's service layer, requesting machines that match the specified capabilities.  
    * The service layer uses the standardized format of Verifiable Credentials (VCs) to search for machines with the required capabilities.  
    * It retrieves a list of DIDs of machines that meet the criteria.  
  * Identity and Capability Verification:  
    * The AI agent establishes connections with the identified machines based on their DIDs.  
    * It verifies the identity and capabilities of each machine by requesting and validating their Verifiable Credentials (VCs).  
    * This verification ensures that the machines can perform the required task accurately and securely.  
  * Request and Response Handling:  
    * Once the AI agent has verified the machines' identities and capabilities, it sends the appropriate requests to the selected machines, providing the necessary input data.  
    * The machines process the requests and generate responses according to their specified output formats.  
    * The AI agent receives the responses from the machines and collects the output.  
  * Result Integration and Presentation:  
    * The AI agent integrates the responses from the machines into a coherent and verified response for the user.  
    * It applies any necessary post-processing, such as summarization or formatting, to ensure the response meets the user's requirements.  
    * The agent presents the final response to the user, providing the requested information or completing the requested task.  
  * User Evaluation:  
    * The user has the option to evaluate the result provided by the AI agent.  
    * They can provide feedback on the accuracy, relevance, or quality of the response, allowing the AI agent to improve its performance over time.

## Advantages of Decentralized M2M Framework for AIs and Services

Machines provide real-time data and services, ensuring access to the most up-to-date information, which is often missing from language model training datasets. This enables AIs and services to deliver accurate and timely results to users. For example, a news aggregation AI can utilize real-time data from registered machines to provide the latest news updates to users.

This framework establishes a foundation for decentralized machine-to-machine collaboration, with a comprehensive system of registration, verification, search, and scoring. It ensures that AIs and services can seamlessly interact and collaborate with each other, expanding the capabilities and possibilities of AI systems. For instance, a machine translation AI can leverage the framework to access specialized language processing AIs for improved translation accuracy.

The use of DIDs, VCs, JWTs, and UUIDs ensures a secure, scalable, and interoperable ecosystem that empowers digital identities and fosters trust among machines. The cryptographic mechanisms employed in the framework protect the integrity and authenticity of data and interactions, while the standardized formats enable seamless communication and compatibility between different AIs and services. This facilitates trust-based collaborations in domains like medical diagnosis, where multiple AI systems can securely share patient data for accurate analysis.

With the capability declaration and user-reported scores, the framework allows users to make informed decisions about which AI or service to utilize based on their specific requirements. Users can evaluate AI models based on benchmark results claimed, user-reported scores, and other metrics. This transparency empowers users to choose the most suitable AI or service for their needs, fostering a competitive and quality-driven ecosystem.

The framework also considers privacy concerns by providing the option to log or not log request and response data. This ensures that users have control over their data and can choose whether or not to retain a record of their interactions with AIs and services. For instance, a privacy-focused AI assistant can utilize this framework to ensure user data stays within the user's control, without compromising on service quality.

## Future Development

### Integration of Payment Ledger:

* By incorporating a payment layer utilizing distributed ledger technology, the framework can facilitate machine-to-machine interaction with seamless support for automatic API credit payment and API handling priorities. This addition enhances the ecosystem by enabling secure and efficient financial transactions between AIs and services. The payment ledger ensures transparent and trustless transactions, fostering a sustainable and incentivized environment for collaboration.

### Incentivizing Additional Nodes:

* To enhance the throughput and distribution of the service layer, a system of incentives can be implemented to encourage users to host their own search nodes. By rewarding users who contribute their resources to the network, such as computational power and storage, the service layer becomes more stable and available. This increased availability and redundancy improve the overall performance and scalability of the framework, enabling a wider range of machines to be discovered and utilized.  
* As an extension of service nodes, other types of nodes can be added later. These nodes play a crucial role in ensuring the health and stability of the decentralized peer-to-peer network by contributing to routing, data hosting, and other essential functions. By providing incentives for hosting gateway nodes, the framework can attract more participants and ensure the continuous availability and reliability of the network.  
* Similar to how Ethereum gas fees work, a mechanism can be implemented to create incomes for those who host nodes. This incentive structure could be designed to reward node operators based on their contributions to the network, such as the amount of data routed, the uptime and reliability of their nodes, and the quality of service provided. By aligning incentives with network health and performance, this approach encourages more individuals and organizations to host gateway nodes, leading to an expanded and robust network infrastructure.

### Standardized Registration Form:

* To maximize interaction and facilitate future improvements, the framework can introduce a standardized registration form. This form would define a set of required fields and key-value pairs that AIs and services must provide during the registration process. Standardization enables compatibility and interoperability among different entities, streamlining the service discovery and collaboration process. With a standardized form, the adoption of the framework by AIs and services would increase, leading to a richer and more diverse ecosystem with expanded functionalities and capabilities.

### Integration of Reputation System:

* Implementing a reputation system within the decentralized ecosystem can enhance trust and reliability among AIs and services. This system would allow users to provide ratings and feedback on the performance and quality of interactions with different entities. By incorporating reputation scores into the service discovery process, users can make more informed decisions when selecting AIs or services to collaborate with, fostering a higher level of accountability and encouraging continuous improvement.

### Expansion of Interoperability:

* To further enhance the ecosystem's capabilities, future development can focus on expanding interoperability with external systems and platforms. This would allow seamless integration and communication between the decentralized framework and other AI ecosystems, data sources, or third-party services. By enabling interoperability, the framework becomes more versatile and adaptable, opening up opportunities for cross-platform collaborations and expanding the range of available AI capabilities.

### Cross-Domain Collaboration:

* Expanding the decentralized ecosystem to support cross-domain collaborations can unlock new possibilities and synergies. By facilitating interactions between AIs and services from diverse domains, such as healthcare, finance, and transportation, the framework can enable cross-pollination of expertise and foster innovative solutions. This cross-domain collaboration can lead to the development of advanced AI systems that address complex challenges and provide holistic solutions across various industries.

## Additional Resources

* Home page: [https://machinetomachine.ai/](https://machinetomachine.ai/)   
* Documentation: [https://machine-to-machine.github.io/](https://machine-to-machine.github.io/)   
* Source code: [https://github.com/Machine-To-Machine/](https://github.com/Machine-To-Machine/)
