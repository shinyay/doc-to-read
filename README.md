# Docs to READ

- [ ] []()
  - []()

## 2025-04

- [x] [Legacy Modernization: Architecting Real-Time Systems Around a Mainframe](https://www.infoq.com/articles/architecting-real-time-systems-around-mainframe/)
  - [infoq]()

## Summary of **“Legacy Modernization: Architecting Real-Time Systems Around a Mainframe”**

### Key Takeaways (from the article)

| # | Point                                                 | Explanation                                                                                                                                                          |
| - | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | **Decouple on three axes**                            | Technical, semantic (DDD), and organisational (Team Topologies) decoupling let National Grid escape a tightly-coupled mainframe without a full rewrite. ([InfoQ][1]) |
| 2 | **Change Data Capture (CDC) ⇒ “System-of-Reference”** | Streaming DB2 changes into Kafka gave near-real-time data to downstream services, eliminating most synchronous mainframe calls. ([InfoQ][1])                         |
| 3 | **GraphQL over REST & BFF sprawl**                    | A stitched GraphQL super-schema let front-ends fetch exactly what they needed and killed dozens of bespoke BFFs. ([InfoQ][1])                                        |
| 4 | **Team Topologies alignment**                         | Stream-aligned, enablement, and complicated-subsystem teams mapped cleanly onto bounded contexts, cutting coordination cost. ([InfoQ][1])                            |
| 5 | **Incremental hybrid rollout**                        | Edge routing and release-train automation enabled a strangler-fig migration—no “big-bang” weekend cut-over. ([InfoQ][1])                                             |

---

## Deep-Dive Insights & Architectural Lessons

### 1. **Treat CDC + Event Streams as the Modern Core**

*CDC isn’t just an “integration trick”; it becomes the heartbeat of your new platform.*

* **Pattern**: Mainframe → CDC → Kafka → Domain processors → Doc DB (Cosmos/Mongo).
* **Why it works**: Read-side scale, graceful degradation when the mainframe is down, and versioned domain models independent of COBOL schemas.
* **Watch-outs**: Batch jobs can flood your stream; throttle or separate “batch” topics from “operational” ones. ([InfoQ][1])

### 2. **DDD + GraphQL = Anti-BFF Medicine**

GraphQL lets each product team compose its *own* view; DDD keeps the schema business-oriented, not mainframe-oriented.

> **Tip:** Start with stitched schemas for speed, but move to *federated* GraphQL once the graph grows—exactly the pain National Grid felt later. ([InfoQ][1])

### 3. **Organisation IS Architecture**

Aligning teams to bounded contexts (Team Topologies) yields:

* Clear ownership of code + schema + SLIs.
* Faster flow with fewer hand-offs.
* A natural “strangler” path—each stream-aligned team decommissions its slice of the monolith as capability migrates. ([InfoQ][1])

### 4. **Anti-Corruption Saga for Write-Backs**

For commands that *must* hit the mainframe (e.g., “Submit Payment”), National Grid wrapped a **parallel saga**:

1. Front-end posts command → orchestrator writes **state-machine doc**.
2. Integration service converts event → mainframe transaction.
3. Mainframe response & CDC update race back.
4. API layer merges *state* + *CDC* to present one consistent view.

That dual-signal reconciliation avoids “ghost payments” and keeps eventual consistency understandable. ([InfoQ][1])

### 5. **Release-Train + Feature Flags → Continuous Strangle**

Thirty-plus repos, trunk-based dev, and a “deployment repo” (Kustomize) let five teams ship together every sprint while routing only a subset of users to UWP 2.0. Value flows; risk stays capped. ([InfoQ][1])

---

## How to Apply These Lessons to *Your* Modernisation

1. **Map coupling hotspots** – Identify synchronous choke-points; target them with CDC first.
2. **Stand up a thin “system-of-reference”** – Even a single high-value aggregate proves the concept.
3. **Bounded-context first, tech second** – Let DDD workshops drive your schema; choose GraphQL/REST afterwards.
4. **Create a mainframe integration team (complicated-subsystem)** – Shield product teams from green-screen nightmares.
5. **Invest in observability on day 1** – Tracing + correlation IDs across event chains is non-negotiable.
6. **Plan for schema evolution** – Versioned events + contract tests keep CDC streams evergreen.
7. **Govern via KPIs, not milestones** – Track call-centre tickets, page-load latency, and mainframe MIPS saved; fund what moves the needle.

---

### Final Thought

Modernising a mainframe isn’t about killing it overnight—it’s about **relentlessly reducing blast-radius and cognitive load** until the legacy core is just another bounded context. National Grid shows that with CDC, event-driven design, and Team Topologies, you can reach cloud-native agility while the mainframe quietly hums in the background.

[1]: https://www.infoq.com/articles/architecting-real-time-systems-around-mainframe/ "Legacy Modernization: Architecting Real-Time Systems Around a Mainframe - InfoQ"


- [x] [AI Trends Disrupting Software Teams](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)
  - [infoq]()

AI is reshaping every corner of the software-delivery pipeline.  Bilgin Ibryam’s InfoQ article distils **five macro-trends**—from “AI-first coding” to agentic systems—that are already disrupting developers, ops, documentation, SaaS products and platform teams.  Each trend removes manual effort from a different layer of work, forcing professionals to up-skill in prompting, orchestration and evaluation to stay valuable.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## 1. Generative Software Development
AI copilots are lifting coding from line-by-line typing to *prompt-driven generation*, able to scaffold components or whole apps from natural language or screenshots.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  Two tool streams are emerging: **IDE copilots** (GitHub Copilot, Cursor) that fit today’s workflows, and **autonomous coding agents** (Devin, v0.dev) that build and run apps in sand-boxed VMs.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  Developers who pivot from “expert typist” to **AI collaborator**—supplying architecture context, refining prompts and validating output—will thrive.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## 2. AI-Powered Operations
Human capacity can’t keep pace with telemetry from cloud-native systems, so observability vendors now embed LLMs for anomaly detection, root-cause analysis and chat-based run-books.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  Ops work shifts from writing queries to **designing AI-guided SLOs and remediation policies**.  Teams must still understand system architecture to approve or override automated fixes.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## 3. Context-Aware Interactive Documentation
Retrieval-Augmented Generation turns static docs into **conversational, code-aware assistants** that surface up-to-date APIs, stack traces and best-practice snippets in chat form.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  Technical writers move from manual updates to curating FAQs, mining incident logs and closing knowledge gaps the AI reveals.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## 4. AI Assistants as the SaaS Interface
Complex serverless and cloud services are exposing **embedded AI side-kicks** (e.g., Supabase AI, Vercel’s v0.dev) that understand the user’s current state and can *execute* actions, not just explain them.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  SaaS vendors that ignore this pattern risk disruption by AI-native competitors with friction-free onboarding.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## 5. Rise of Agentic Systems
The frontier is networks of autonomous agents (AutoGPT, LangGraph, Dapr Agents) that plan, coordinate and carry out multi-step business tasks.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))  Success demands new skills: agent design patterns, LLM observability, secure orchestration and continuous evaluation.  Organisations must either up-skill existing teams or hire talent fluent in agentic architectures.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/))

## How to Respond
| Role | Adaptation playbook |
|------|--------------------|
| **Developers** | Master prompt-engineering, system design and AI code-review; treat copilots as partners, not oracles.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)) |
| **Ops / SRE** | Deploy AI-driven observability, automate first-line remediation, keep humans in the escalation loop.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)) |
| **Tech writers** | Use AI to generate drafts, focus on dynamic content and conversation flows.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)) |
| **SaaS PMs** | Embed context-aware assistants, rethink product-led growth funnels around natural-language UIs.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)) |
| **Architects / Platform Eng.** | Learn agent orchestration frameworks, build golden paths for AI workloads, instrument LLM metrics.  ([AI Trends Disrupting Software Teams - InfoQ](https://www.infoq.com/articles/ai-trends-disrupting-software-teams/)) |

**Bottom line:** AI will not replace software teams, but teams that learn to *delegate wisely* to AI—coding, ops, docs, SaaS UX and multi-agent coordination—will outpace those that don’t.


## 2025-03

- [x] [Getting Started: Model Context Protocol](https://medium.com/@kenzic/getting-started-model-context-protocol-e0a80dddff80)

>### Detailed Summary of the Article on MCP
>
>#### Introduction
>- **MCP Overview**: The Model Context Protocol (MCP) is designed to simplify AI integrations, break down data silos, and unlock real-time data access. It aims to provide a universal standard for connecting AI to various data sources and tools.
>
>#### Key Features and Benefits
>- **Simplified Integrations**: MCP eliminates the need for custom integrations for each new data source, making it easier for AI systems to access the necessary context.
>- **Real-Time Data Access**: By connecting AI to data sources in real-time, MCP enhances the relevance and quality of AI outputs.
>- **User-Friendly**: MCP allows users to interact with data systems using natural language, automating repetitive tasks and combining various actions to save time.
>
>#### How MCP Works
>- **Architecture**: MCP bridges two key components: MCP servers that expose data sources and MCP clients (AI apps) that connect to those servers. This setup allows AI systems to access data and tools in real-time while maintaining a permissions framework to control access.
>- **Components**:
>  - **Hosts**: LLM applications that initiate connections.
>  - **Clients**: Maintain 1:1 connections with servers inside the host application.
>  - **Servers**: Provide context, tools, and prompts to clients.
>
>#### Practical Applications
>- **Task Automation**: MCP is used to automate tasks, manage data, and enhance productivity across different industries.
>- **Versatility**: It connects with various databases (e.g., PostgreSQL, MySQL, SQLite) and platforms (e.g., GitHub, Slack, Gmail), making AI a versatile assistant capable of handling multiple tasks efficiently.
>
>#### Innovations
>- **Unified Framework**: MCP standardizes AI interactions with external tools and systems, eliminating the need for custom integrations.
>- **Communication Methods**: Supports various communication methods like Standard Input/Output (STDIO) and Server-Sent Events (SSE), enabling real-time updates and reducing delays.
>
>#### Future Prospects
>- **Potential Adoption**: MCP has the potential to become a fundamental standard for AI connectivity, similar to USB-C for devices. Its success will depend on its adaptability to evolving AI technologies and user needs.
>

- [x] [The open source Model Context Protocol was just updated — here’s why it’s a big deal](https://venturebeat.com/ai/the-open-source-model-context-protocol-was-just-updated-heres-why-its-a-big-deal/)

>### Detailed Summary of the Article on MCP
>
>#### Introduction
>- **MCP Milestone**: The Model Context Protocol (MCP) has reached a significant milestone with an updated version, enhancing AI agents' security, capabilities, and >interoperability.
>- **OpenAI's Support**: OpenAI announced support for MCP across its products, including the Agents SDK and upcoming support for ChatGPT's desktop app and Responses API.
>
>#### Key Updates in MCP
>- **OAuth 2.1-Based Authorization Framework**: Introduces a robust standard for securing agent-server communication.
>- **Streamable HTTP Transport**: Replaces the older HTTP+SSE setup, enabling real-time, bidirectional data flow.
>- **JSON-RPC Batching**: Allows multiple requests to be sent in one go, improving efficiency.
>- **Tool Annotations**: Adds rich metadata for describing tool behavior, enhancing AI agents' discovery and reasoning capabilities.
>
>#### Microsoft's Contribution
>- **Playwright-MCP**: Microsoft released Playwright-MCP, enabling AI agents to interact with web pages using the Chrome accessibility tree. This allows AI agents to navigate, >click, type, and interact with web content like real users.
>
>#### Broader Implications
>- **Interoperability**: MCP aims to standardize AI interactions with tools and systems, making it easier for AI agents to work across different platforms.
>- **Industry Support**: With backing from companies like Anthropic, LangChain, and now Microsoft, MCP is poised to become a standard for AI connectivity.
>
>#### Future Prospects
>- **Potential Adoption**: If other major players like Meta, Amazon, or Apple adopt MCP, it could become the universal "language" for AI actions, significantly advancing AI interoperability.


- [x] [OpenAI adopts rival Anthropic’s standard for connecting AI models to data](https://techcrunch.com/2025/03/26/openai-adopts-rival-anthropics-standard-for-connecting-ai-models-to-data/)

>### Detailed Summary of the Article on MCP
>
>#### Introduction
>- **OpenAI Adopts MCP**: OpenAI has decided to support Anthropic's Model Context Protocol (MCP), a standard for connecting AI models to data systems, across its products, >including the ChatGPT desktop app.
>
>#### Key Features of MCP
>- **Enhanced AI Responses**: MCP helps AI models produce more relevant responses by drawing data from various sources like business tools and content repositories.
>- **Two-Way Connections**: Developers can build connections between data sources and AI applications, enabling more dynamic interactions.
>
>#### Adoption and Integration
>- **Industry Adoption**: Since its open-source release, MCP has been adopted by companies like Block, Apollo, Replit, Codeium, and Sourcegraph.
>- **OpenAI's Integration**: OpenAI plans to integrate MCP into its Agents SDK and Responses API, enhancing the functionality of its AI models.
>
>#### Future Plans
>- **Expansion**: OpenAI intends to share more details about its MCP integration plans in the coming months, indicating a broader adoption and potential new features.


- [x] [New Protocol MCP Helps to Transform AI Agents from Isolated Chatbots into Context-Aware Digital Environments](https://www.anoopcnair.com/new-protocol-mcp-helps-to-transform-ai-agents-f/)

>### Detailed Summary of the Article on MCP
>
>#### Introduction to MCP
>- **MCP Overview**: The Model Context Protocol (MCP) is a significant advancement in how systems and users interact with data. It aims to make data interactions more user-friendly, secure, and efficient.
>- **Purpose**: MCP simplifies the process of interacting with complex systems using natural language, making it accessible even to non-tech experts.
>
>#### Key Features and Benefits
>- **User-Friendly Interactions**: MCP allows users to interact with data systems using simple language, automating repetitive tasks and combining various actions to save time.
>- **Security**: MCP ensures data safety by verifying actions before execution, maintaining compliance with security protocols.
>
>#### Functionality
>- **Integration with Tools and APIs**: MCP connects AI systems to data systems and APIs, such as Microsoft Graph, enabling agents to process commands, retrieve information, and modify data based on user context.
>- **Example - Lokka**: Lokka is an MCP for Microsoft Graph that allows users to manage tasks and data using natural language commands, streamlining operations without complex setups.
>
>#### Innovations
>- **Unified Framework**: MCP standardizes AI interactions with external tools and systems, eliminating the need for custom integrations. This makes it easier to connect AI with databases, APIs, and other platforms.
>- **Communication Methods**: MCP supports various communication methods like Standard Input/Output (STDIO) and Server-Sent Events (SSE), enabling real-time updates and reducing delays.
>
>#### Practical Applications
>- **Task Automation**: MCP is already being used to automate tasks, manage data, and enhance productivity across different industries.
>- **Versatility**: It connects with various databases (e.g., PostgreSQL, MySQL, SQLite) and platforms (e.g., GitHub, Slack, Gmail), turning AI into a versatile assistant capable of handling multiple tasks efficiently.
>
>#### Conclusion
>- **Future Potential**: MCP has the potential to become a fundamental standard for AI connectivity, similar to USB-C for devices. Its success will depend on its adaptability to evolving AI technologies and user needs.


- [x] [Model Context Protocol — Intuitively and Exhaustively Explained](https://iaee.substack.com/p/model-context-protocol-intuitively)

>### Introduction to MCP
>- **MCP Overview**: MCP is a new standard allowing AI to connect with external systems, similar to how humans use web browsers. It's often described as the "HTTP of AI" due to >its potential to revolutionize AI connectivity.
>- **Popularity**: The protocol has seen rapid growth and is considered a significant advancement in AI integration.
>
>### Key Concepts and Technologies
>- **Retrieval Augmented Generation (RAG)**: A method to inject contextual information into AI models, enhancing their ability to answer specific queries.
>- **Agents**: Extensions of RAG that use tools to execute tasks, making AI interactions more dynamic and functional.
>
>### Anthropic and MCP
>- **Anthropic's Role**: The company behind MCP, known for its Claude family of models. They aim to improve AI integration with desktop environments through MCP.
>- **Claude Desktop**: An application that allows Claude to automate desktop tasks, demonstrating the practical use of MCP.
>
>### MCP Functionality
>- **Tools, Resources, and Prompts**: MCP standardizes how AI models access and use external data and tools.
>  - **Tools**: Functions that AI models can execute.
>  - **Resources**: Data that can be read by AI models.
>  - **Prompts**: Pre-written templates to guide AI interactions.
>
>### Advanced Features
>- **Resource Templates**: Allow dynamic querying of resources.
>- **Sampling**: Enables servers to request LLM completions through the client.
>- **Roots**: Define the boundaries where servers can operate, ensuring security and privacy.
>
>### Transports
>- **Standard Input/Output (stdio)**: The default transport method for local communication.
>- **Server Side Events (SSE)**: Allows MCP clients and servers to communicate over the internet, enabling broader connectivity.
>
>### Closing Thoughts
>- **Future of MCP**: While MCP is still in its early stages, it has the potential to become a fundamental standard for AI connectivity, similar to USB-C for devices. However, >its future depends on how well it adapts to evolving AI technologies and user needs.

## 2025-01

- [ ] [Developer Productivity: Who’s Tracking It? Not Many](https://thenewstack.io/developer-productivity-whos-tracking-it-not-many/)
  - [thenewstack]()
  - > - **Tracking Developer Productivity**: Only 28% of managers surveyed measure both developer productivity and experience, while 40% measure neither.
    > - **Satisfaction Levels**: Among managers aware of their company's approach, 57% are satisfied with how developer productivity and experience are tracked.
    > - **Role Awareness**: 60% of those responsible for developer productivity/experience are aware of their company's approach, but only 35% stay informed about the latest trends.
    > - **Survey Details**: The report surveyed over 23,000 developers worldwide.

Would you like more details on any specific aspect?

- [ ] [5 Steps to Build a Standardized Software Development Platform](https://thenewstack.io/5-steps-to-build-a-standardized-software-development-platform/)
  - [thenewstack]()

- [ ] [Five Ways Your Platform Engineering Journey Can Derail](https://thenewstack.io/five-ways-your-platform-engineering-journey-can-derail/)
  - [thenewstack]()

- [ ] [What 2024’s Data Told Us About How Developers Work Now](https://thenewstack.io/what-2024s-data-told-us-about-how-developers-work-now/)
  - [thenewstack]()

- [x] [Developer Productivity in 2025: More AI, but Mixed Results](https://thenewstack.io/developer-productivity-in-2025-more-ai-but-mixed-results/)
  - [thenewstack]()
  - > - **AI Adoption**: In 2024, generative AI was widely adopted for software development, but it didn't significantly improve developer productivity due to technical debt and documentation issues.
    > - **Security Risks**: Increased AI-generated code has led to more security vulnerabilities, requiring better tools for managing and validating code.
    > - **Observability**: The complexity of AI-driven code generation necessitates robust observability tools to maintain efficiency and quality.
    > - **Team Dynamics**: AI is expected to change team organization, with AI assistants becoming integral to workflows.
    > - **Junior Developers**: Early-career developers face challenges due to the gap between education and real-world skills, and the rise of AI might exacerbate this issue.
    > - **Upskilling**: Continuous training is essential for both junior and senior developers to effectively use AI tools.

Let me know if you need more details on any specific section!
## 2024-12

- [ ] [4 North Star Metrics for Platform Engineering Teams](https://thenewstack.io/4-north-star-metrics-for-platform-engineering-teams/)
  - [thenewstack]()

- [ ] [6 Steps To Shift Platform Engineering From Reactive to Proactive](https://thenewstack.io/6-steps-to-shift-platform-engineering-from-reactive-to-proactive/)
  - [thenewstack]()

- [ ] [DORA 2024: AI and Platform Engineering Fall Short](https://thenewstack.io/dora-2024-ai-and-platform-engineering-fall-short/)
  - [thenewstack]()


## 2024-11

## 2024-10

- [ ] [Azure Spring Boot](https://github.com/microsoft/azure-spring-boot)
  - [github]()

- [ ] [Spring Cloud Azure modules](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/spring)
  - [github]()

- [ ] [Spring Cloud Azure Samples](https://github.com/Azure-Samples/azure-spring-boot-samples)
  - [github]()

- [ ] [Spring Cloud Azure documentation - JP](https://learn.microsoft.com/ja-jp/azure/developer/java/spring-framework/)
  - [mslean]()

- [ ] [Spring Cloud Azure - Reference Documentation](https://microsoft.github.io/spring-cloud-azure/current/reference/html/index.html)
  - [github]()

- [ ] [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java/)
  - [github]()

- [ ] [Spring Cloud Azure](https://github.com/microsoft/spring-cloud-azure)
  - [github]()

- [ ] [Spring Cloud Azure documentation](https://learn.microsoft.com/en-us/azure/developer/java/spring-framework/)
  - [mslearn]()

- [ ] [Microsoft Taking Up the Mantra of Platform Engineering](https://thenewstack.io/microsoft-taking-up-the-mantra-of-platform-engineering/)
  - [thenewstack]()

- [ ] [Build Platform Engineering as a Product for Dev Adoption](https://thenewstack.io/build-platform-engineering-as-a-product-for-dev-adoption/)
  - [thenewstack]()

- [ ] [How Supabase Is Building Its Platform Engineering Strategy](https://thenewstack.io/how-supabase-is-building-its-platform-engineering-strategy/)
  - [thenewstack]()

- [ ] [How to Build an Internal Developer Platform Like a Product](https://thenewstack.io/how-to-build-an-internal-developer-platform-like-a-product/)
  - [thenewstack]()

## 2024-09

- [ ] [Open Source Culture Starts with Programs and Policies](https://thenewstack.io/open-source-culture-starts-with-programs-and-policies/)
  - [thenewstack]()

- [ ] [Adopting an ‘Inner Source’ Culture Within Organizations](https://thenewstack.io/adopting-inner-source-culture-within-organizations/)
  - [thenewstack]()

- [ ] [Innersource: Building Open Source Projects Behind Company Firewalls](https://thenewstack.io/github-bloomberg-talk-using-innersource-build-open-source-project-development-behind-company-firewalls/)
  - [thenewstack]()

- [ ] [How To Implement InnerSource With an Internal Developer Portal](https://thenewstack.io/how-to-implement-innersource-with-an-internal-developer-portal/)
  - [thenewstack]()

- [ ] [Building a platform engineering team that’s set up for success](https://sdtimes.com/softwaredev/building-a-platform-engineering-team-thats-set-up-for-success/)
  - [sdtimes]()

- [ ] [Platform Engineering Is Security Engineering](https://www.darkreading.com/application-security/platform-engineering-is-security-engineering)
  - [misc]()

- [ ] [How Supabase Is Building Its Platform Engineering Strategy](https://thenewstack.io/how-supabase-is-building-its-platform-engineering-strategy/)
  - [thenewstack]()

- [ ] [Platform Engineering – Making Other Teams 10x Better](https://www.infoq.com/podcasts/platform-engineering-teams-10x-better/)
  - [infoq]()

- [ ] [Platform tooling landscape](https://platformengineering.org/platform-tooling)
  - ![image](https://cdn.prod.website-files.com/6489de99f6259b6eef4fae4f/66cefbd4024c2bf8e2a844c0_platform-tooling-landscape-2024-08-15-p-1600.webp)

## 2024-08

- [ ] [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow)
  - [github docs]()

- [ ] [Beginner’s guide to GitHub: Adding code to your repository](https://github.blog/developer-skills/github/beginners-guide-to-github-adding-code-to-your-repository/)
  - [github]()

- [ ] [How to use AI coding tools to learn a new programming language](https://github.blog/developer-skills/programming-languages-and-frameworks/how-to-use-ai-coding-tools-to-learn-a-new-programming-language/)
  - [github]()

- [ ] [What’s new with GitHub Copilot: July 2024](https://github.blog/ai-and-ml/github-copilot/whats-new-with-github-copilot-july-2024/)
  - [github]()

- [ ] [Introducing GitHub Models: A new generation of AI engineers building on GitHub](https://github.blog/news-insights/product-news/introducing-github-models/)
  - [github]()

- [ ] [https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/](https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)
  - [github]()

- [ ] [DORA, SPACE, and DevEx: Choosing the right framework](https://getdx.com/podcast/dora-space-devex-choosing-framework/)
  - [engineeringenablement]()

- [ ] [How to measure GenAI adoption and impact](https://getdx.com/podcast/how-to-measure-genai-adoption-impact/)
  - [engineeringenablement]()

- [ ] [Get Certified in Platform Engineering, Starting Aug. 6]()
  - [thenewstack](https://thenewstack.io/get-certified-in-platform-engineering-starting-aug-6/)

- [ ] [Score: New CNCF Sandbox Tool for Infrastructure-Centric Dev]()
  - [thenewstack](https://thenewstack.io/score-new-cncf-sandbox-tool-for-infrastructure-centric-dev/)

## 2024-07

- [ ] [DevEx Quick Wins for Platform Team Success]()
  - [thenewstack](https://thenewstack.io/platform-teams-win-over-devs-with-quick-wins/)

- [ ] [How To Run Databases in Kubernetes]()
  - [thenewstack](https://thenewstack.io/how-to-run-databases-in-kubernetes/)

- [ ] [How To Run WebAssembly on Kubernetes]()
  - [thenewstack](https://thenewstack.io/how-to-run-webassembly-on-kubernetes/)

- [ ] [Copilot text completion for pull request descriptions beta]()
  - [github](https://github.blog/changelog/2024-07-24-copilot-text-completion-for-pull-request-descriptions-beta/)

- [ ] [How to review code effectively: A GitHub staff engineer’s philosophy]()
  - [github](https://github.blog/developer-skills/github/how-to-review-code-effectively-a-github-staff-engineers-philosophy/)

- [ ] [Internal Developer Platforms: The Heart of Platform Engineering]()
  - [thenewstack](https://thenewstack.io/internal-developer-platforms-the-heart-of-platform-engineering/)

- [ ] [Platform Engineering Can Help Your Security Team, Too]()
  - [thenewstack](https://thenewstack.io/platform-engineering-can-help-your-security-team-too/)

- [ ] [Platform Engineering: It Is All About the Tooling]()
  - [thenewstack](https://thenewstack.io/platform-engineering-it-is-all-about-the-tooling/)

- [ ] [What’s the Impact of Platform Engineering?]()
  - [thenewstack](https://thenewstack.io/platformcon-whats-the-impact-of-platform-engineering/)

- [ ] [The Hidden Benefits of Internal Developer Platforms]()
  - [thenewstack](https://thenewstack.io/the-hidden-benefits-of-internal-developer-platforms/)

- [ ] [Platform Engineering Is for Everyone]()
  - [thenewstack](https://thenewstack.io/platform-engineering-is-for-everyone/)

- [ ] [How To Measure Platform Engineering]()
  - [thenewstack](https://thenewstack.io/how-to-measure-platform-engineering/)

- [ ] [Why Internal Developer Portals Need Automations]()
  - [thenewstack](https://thenewstack.io/why-internal-developer-portals-need-automations/)

- [ ] [IDP vs. Self-Service Portal: A Platform Engineering Showdown]()
  - [thenewstack](https://thenewstack.io/idp-vs-self-service-portal-a-platform-engineering-showdown/)

## 2024-06

- [ ] [Composable Platforms Are Promising, but Not a Silver Bullet]()
  - [thenewstack](https://thenewstack.io/composable-platforms-are-promising-but-not-a-silver-bullet/)

- [ ] [How Do You Measure Developer Experience?]()
  - [thenewstack](https://thenewstack.io/how-do-you-measure-developer-experience/)

- [ ] [Internal Developer Platform vs. Internal Developer Portal: What’s Up?]()
  - [thenewstack](https://thenewstack.io/internal-developer-platform-vs-internal-developer-portal-whats-up/)

- [ ] [7 Principles for Improving Software Delivery]()
  - [thenewstack](https://thenewstack.io/agile-devops-platform-engineering-confusion-stalls-devs/)

- [ ] [Boost Developer Productivity by Reducing Their ‘Paper Cuts’]()
  - [thenewstack](https://thenewstack.io/boost-developer-productivity-by-reducing-their-paper-cuts/)

- [ ] [Tips for Building a Platform Engineering Discipline That Lasts]()
  - [thenewstack](https://thenewstack.io/tips-for-building-a-platform-engineering-discipline-that-lasts/)

- [ ] [Platform Engineering for a Mainframe: Design Thinking Drives Change]()
  - [thenewstack](https://thenewstack.io/platform-engineering-for-a-mainframe-design-thinking-drives-change/)

- [ ] [Platform Engineering for a Mainframe: Design Thinking Drives Change]()
  - [thenewstack](https://thenewstack.io/platform-engineering-for-a-mainframe-design-thinking-drives-change/)

- [ ] [API Trends: Platform Engineering, the Unbundling and AI’s Role]()
  - [thenewstack](https://thenewstack.io/api-trends-platform-engineering-the-unbundling-and-ais-role/)

- [ ] [This Is Why Infra Teams Should Care About Platform Engineering]()
  - [thenewstack](https://thenewstack.io/this-is-why-infra-teams-should-care-about-platform-engineering/)

- [ ] [https://thenewstack.io/new-spotify-portal-for-backstage-eases-platform-engineering/]()
  - [thenewstack](https://thenewstack.io/new-spotify-portal-for-backstage-eases-platform-engineering/)

- [ ] [Platform Engineering: What Does ‘Good’ Look Like?]()
  - [thenewstack](https://thenewstack.io/platform-engineering-what-does-good-look-like/)

- [ ] [DevEx Success: How Pfizer Scaled to 1,000 Engineers]()
  - [thenewstack](https://thenewstack.io/devex-success-how-pfizer-scaled-to-1000-engineers/)

- [ ] [AI in Platform Engineering: Concerns Grow Alongside Advantages]()
  - [thenewstack](https://thenewstack.io/ai-in-platform-engineering-concerns-grow-alongside-advantages/)

- [ ] [Your Engineering Organization Is Too Expensive]()
  - [thenewstack](https://thenewstack.io/your-engineering-organization-is-too-expensive/)

- [ ] [Drive Developer Self-Service with Crossplane, K8s and a Portal]()
  - [thenewstack](https://thenewstack.io/drive-developer-self-service-with-crossplane-k8s-and-a-portal/)

- [ ] [Unlocking the power of unstructured data with RAG]()
  - [github](https://github.blog/2024-06-13-unlocking-the-power-of-unstructured-data-with-rag/)

- [ ] [How we improved push processing on GitHub]()
  - [github](https://github.blog/2024-06-11-how-we-improved-push-processing-on-github/)


- [ ] [Top 12 Git commands every developer must know]()
  - [github](https://github.blog/2024-06-10-top-12-git-commands-every-developer-must-know/)

- [ ] [Arm64 on GitHub Actions: Powering faster, more efficient build systems]()
  - [github](https://github.blog/2024-06-03-arm64-on-github-actions-powering-faster-more-efficient-build-systems/)

- [ ] [GitHub and JFrog partner to unify code and binaries for DevSecOps]()
  - [github](https://github.blog/2024-05-29-github-and-jfrog/
  )

## 2024-05

### Platform Engineering

- [ ] [What Comes after Internal Developer Platforms?]()
  - [thenewstack](https://thenewstack.io/what-comes-after-internal-developer-platforms/)

- [ ] [Unleash AI in Platform Engineering to Streamline Software Delivery]()
  - [thenewstack](https://thenewstack.io/integrating-ai-to-make-platform-engineering-intelligent/)

### Spring AI

- [x] [LLM Applications with Java and Spring AI]()
  - [github](https://github.com/ThomasVitale/llm-apps-java-spring-ai)

- [x] [Spring AI Introduction: Building AI Applications in Java with Spring]()
  - [youtube](https://www.youtube.com/watch?v=yyvjT0v3lpY&list=PLZV0a2jwt22uoDm3LNDFvN6i2cAVU_HTH)

- [x] [Spring AI - Structured Output]()
  - [spring](https://spring.io/blog/2024/05/09/spring-ai-structured-output)

- [x] [Spring AI - Multimodality - Orbis Sensualium Pictus]()
  - [spring](https://spring.io/blog/2024/04/19/spring-ai-multimodality-orbis-sensualium-pictus)

- [x] [Getting Started with Spring AI and Azure Open AI (Jan-3)]()
  - [youtube](https://www.youtube.com/watch?v=RoAyxO_0IxM)

- [x] [Paving a Painless Path to Production AI in Your Java Applications - Mark Heckler (Apr-24)]()
  - [youtube](https://www.youtube.com/watch?v=r_GqXc3Q-bU)

- [x] [Refactoring a Spring AI Proof of Concept (PoC) - Part 1: Covering with tests]()
  - [youtube](https://www.youtube.com/watch?v=lV3IUT5VxqA)

- [x] [Four Cool Things About Spring AI]()
  - [youtube](https://www.youtube.com/watch?v=HjDucvwmWeE)

- [x] [Spring Boot conformity Spring AI Implement project access to chatgpt]()
  - [dev](https://dev.to/superhandsomeg/spring-boot-conformity-spring-ai-implement-project-access-to-chatgpt-4opp)

- [x] [Getting started with Spring AI]()
  - [dev](https://dev.to/anthonyikeda/getting-started-with-spring-ai-4j09)

- [x] [Spring Tips: Spring AI]()
  - [youtube](https://www.youtube.com/watch?v=aNKDoiOUo9M)

- [x] [Spring AI 1.0.0-SHAOSHOT]()
  - [spring](https://docs.spring.io/spring-ai/reference/1.0-SNAPSHOT/index.html)

## 2024-04

- [ ] [Platform Engineering and GenAI: ‘Get Your House in Order’]()
  - [thenewstack](https://thenewstack.io/platform-engineering-and-genai-get-your-house-in-order/)

- [ ] [How Platform Engineering Takes on DevOps Challenges]()
  - [thenewstack](https://thenewstack.io/how-platform-engineering-takes-on-devops-challenges/)

- [ ] [Developer Joy is the Productivity Metric You’re Missing]()
  - [thenewstack](https://thenewstack.io/how-intercom-ships-industry-leading-developer-experience/)

- [ ] [Platform Engineering: More Teams Now Running 3 or More IDPs]()
  - [thenewstack](https://thenewstack.io/platform-engineering-more-teams-now-running-3-or-more-idps/)

- [ ] [Using an Internal Developer Portal for FinOps Visibility]()
  - [thenewstack](https://thenewstack.io/using-an-internal-developer-portal-for-finops-visibility/)

- [ ] [Platform Engineering Is Not Just about the Tools]()
  - [thenewstack](https://thenewstack.io/platform-engineering-is-not-just-about-the-tools/)

- [ ] [Platform as a Product in 4 Steps]()
  - [thenewstack](https://thenewstack.io/platform-as-a-product-in-4-steps/)

- [ ] [How Spring and Java Shaped Internal Developer Platforms]()
  - [thenewstack](https://thenewstack.io/how-spring-and-java-shaped-internal-developer-platforms/)

- [ ] [AI, LLMs and Security: How to Deal with the New Threats ]()
  - [thenewstack](https://thenewstack.io/ai-llms-and-security-how-to-deal-with-the-new-threats/)

- [ ] [A Coder Perspective: What It’s Like to Develop an AI App]()
  - [thenewstack](https://thenewstack.io/a-coder-perspective-what-its-like-to-develop-an-ai-app/)

- [ ] [JavaScript, Python Neck and Neck in GitHub Developer Usage]()
  - [thenewstack](https://thenewstack.io/javascript-python-neck-and-neck-in-github-developer-usage/)

- [ ] [How Generative AI Coding Assistants Increase Developer Velocity]()
  - [thenewstack](https://thenewstack.io/how-generative-ai-coding-assistants-increase-developer-velocity/)

- [ ] [Shifting Left Is Now Mainstream for Developers, or Is It?]()
  - [thenewstack](https://thenewstack.io/shifting-left-is-now-mainstream-for-developers-or-is-it/)

- [ ] [AI Code Generation: 6 FAQs for Developers]()
  - [thenewstack](https://thenewstack.io/ai-code-generation-6-faqs-for-developers/)

- [ ] [Testing Copilot and ChatGPT as Coding Assistants: What We Found]()
  - [thenewstack](https://thenewstack.io/testing-copilot-and-chatgpt-as-coding-assistants-what-we-found/)

- [ ] [Are Copilots Ready to Provision Your Infrastructure?]()
  - [thenewstack](https://thenewstack.io/are-copilots-ready-to-provision-your-infrastructure/)

- [ ] [Copilot Enterprise Introduces Search and Customized Best Practices]()
  - [thenewstack](https://thenewstack.io/copilot-enterprise-introduces-search-and-customized-best-practices/)

- [ ] [How AI Is Shifting Developer Culture and Work at GitHub]()
  - [thenewstack](https://thenewstack.io/how-ai-is-shifting-developer-culture-and-work-at-github/)

- [ ] [Generative AI Tools for Infrastructure as Code]()
  - [thenewstack](https://thenewstack.io/generative-ai-tools-for-infrastructure-as-code/)

- [ ] [Accessing Perplexity Online LLMs Programmatically Via API]()
  - [thenewstack](https://thenewstack.io/accessing-perplexity-online-llms-programmatically-via-api/)

- [ ] [Dev News: Python AI Tool, a Copilot Alternative, and RSC News]()
  - [thenewstack](https://thenewstack.io/dev-news-python-ai-tool-a-copilot-alternative-and-rsc-news/)

- [ ] [Developer Productivity in 2024: New Metrics, More GenAI]()
  - [thenewstack](https://thenewstack.io/developer-productivity-in-2024-new-metrics-more-genai/)

- [ ] [Generative AI: In 2023, GenAI Tools Became Table Stakes]()
  - [thenewstack](https://thenewstack.io/generative-ai-in-2023-genai-tools-became-table-stakes/)

- [ ] [GitHub Developer Productivity at 30 Billion Messages per Day]()
  - [thenewstack](https://thenewstack.io/github-developer-productivity-at-30-billion-messages-per-day/)
## 2024-01

- [ ] [WebAssembly in 2024: Components Are and Are Not the Big Story]()
  - [thenewstack](https://thenewstack.io/webassembly-in-2024-components-are-and-are-not-the-big-story/)

- [ ] [WebAssembly: 4 Predictions for 2024]()
  - [thenewstack](https://thenewstack.io/webassembly-4-predictions-for-2024/)

- [ ] [Observability in 2024: More OpenTelemetry, Less Confusion]()
  - [thenewstack](https://thenewstack.io/observability-in-2024-more-opentelemetry-less-confusion/)

- [ ] [Web Dev 2024: Fediverse Ramps Up, More AI, Less JavaScript]()
  - [thenewstack](https://thenewstack.io/web-dev-2024-fediverse-ramps-up-more-ai-less-javascript/)

- [ ] [Kubernetes 1.29 ‘Mandala’ Tests Mutable Pod Resources]()
  - [thenewstack](https://thenewstack.io/kubernetes-1-29-mandala-tests-mutable-pod-resources/)

## 2023-12

- [ ] [State of Serverless Computing and Event Streaming in 2024]()
  - [thenewstack](https://thenewstack.io/docker-buys-atomicjar-to-spur-dev-led-integration-testing/)
  - [thenewstack](https://thenewstack.io/state-of-serverless-computing-and-event-streaming-in-2024/)

- [ ] [Docker Buys AtomicJar to Spur Dev-Led Integration Testing]()
  - [thenewstack](https://thenewstack.io/docker-buys-atomicjar-to-spur-dev-led-integration-testing/)

- [ ] [Best of 2023: The End of Programming Is Nigh]()
  - [thenewstack](https://thenewstack.io/the-end-of-programming-is-nigh/)

- [ ] [What Is a WebAssembly Component? The Ultimate Guide]()
  - [thenewstack](https://thenewstack.io/what-is-a-webassembly-component-the-ultimate-guide/)

- [ ] [Year in Review: Platform Engineering Still Run By Spreadsheet]()
  - [thenewstack](https://thenewstack.io/year-in-review-platform-engineering-still-run-by-spreadsheet/)

- [ ] [How to Get Advantages of TypeScript in JavaScript]()
  - [thenewstack](https://thenewstack.io/how-to-get-advantages-of-typescript-in-javascript/)

- [ ] [Generative AI: In 2023, GenAI Tools Became Table Stakes]()
  - [thenewstack](https://thenewstack.io/generative-ai-in-2023-genai-tools-became-table-stakes/)

- [ ] [Year-in-Review: 2023 Was a Turning Point for Microservices]()
  - [thenewstack](https://thenewstack.io/year-in-review-was-2023-a-turning-point-for-microservices/)

- [ ] [Year in Review: GenAI Exposed Silicon Valley Chip Antiquity]()
  - [thenewstack](https://thenewstack.io/year-in-review-genai-exposed-silicon-valley-chip-antiquity/)

- [ ] [Platform Engineering in 2023: Dev First, Collaboration and APIs]()
  - [thenewstack](https://thenewstack.io/platform-engineering-in-2023-dev-first-collaboration-and-apis/)

## 2023-10

### Platform Engineering

- [ ] [Making the Leap: Ops Roles Evolve into Platform Engineers]()
  - [thenewstack](https://thenewstack.io/making-the-leap-ops-roles-evolve-into-platform-engineers/)

- [ ] [Humanitec: The Golden Path to Platform Engineering]()
  - [thenewstack](https://thenewstack.io/humanitec-the-golden-path-to-platform-engineering/)

- [ ] [The Pillars of Platform Engineering: Part 6 — Observability]()
  - [thenewstack](https://thenewstack.io/the-pillars-of-platform-engineering-part-6-observability/)

- [ ] [Software Delivery Enablement, Not Developer Productivity]()
  - [thenewstack](https://thenewstack.io/software-delivery-enablement-not-developer-productivity/)

- [ ] [The Pillars of Platform Engineering: Part 5 — Orchestration]()
  - [thenewstack](https://thenewstack.io/the-pillars-of-platform-engineering-part-5-orchestration/)

- [ ] [Platform Engineering Helps a Scale-up Tame DevOps Complexity]()
  - [thenewstack](https://thenewstack.io/platform-engineering-helps-a-scale-up-tame-devops-complexity/)

## 2023-09

### WebAssembly

- [ ] [What Is WebAssembly?]()
  - [thenewstack](https://thenewstack.io/what-is-webassembly-wasm/)

- [ ] [Can WebAssembly Get Its Act Together for a Component Model?]()
  - [thenewstack](https://thenewstack.io/can-webassembly-get-its-act-together-for-a-component-model/)

- [ ] [WebAssembly Reaches a Cloud Native Milestone]()
  - [thenewstack](https://thenewstack.io/webassembly-reaches-a-cloud-native-milestone/)

- [ ] [Is It too Early to Leverage AI for WebAssembly?]()
  - [thenewstack](https://thenewstack.io/is-it-too-early-to-leverage-ai-for-webassembly/)

- [ ] [Rust and C++ Work Better for WebAssembly]()
  - [thenewstack](https://thenewstack.io/rust-and-c-work-better-for-webassembly/)

- [ ] [Where Does WebAssembly Fit in the Cloud Native World?]()
  - [thenewstack](https://thenewstack.io/where-does-webassembly-fit-in-the-cloud-native-world/)

### Platform Engineering

- [ ] [The Pillars of Platform Engineering: Part 4 — Connectivity]()
  - [thenewstack](https://thenewstack.io/the-pillars-of-platform-engineering-part-4-connectivity/)

- [ ] [Why You Can’t Go from Zero to Platform Engineering]()
  - [thenewstack](https://thenewstack.io/why-you-cant-go-from-zero-to-platform-engineering/)

- [ ] [The Pillars of Platform Engineering: Part 3 — Provisioning]()
  - [thenewstack](https://thenewstack.io/the-pillars-of-platform-engineering-part-3-provisioning/)

- [ ] [A Practical Step-by-Step Approach to Building a Platform]()
  - [thenewstack](https://thenewstack.io/a-practical-step-by-step-approach-to-building-a-platform/)

- [ ] [The 6 Pillars of Platform Engineering: Part 2 — CI/CD & VCS Pipeline]()
  - [thenewstack](https://thenewstack.io/the-6-pillars-of-platform-engineering-part-2-ci-cd-vcs-pipeline/)

- [ ] [CloudBees Scales Jenkins, Redefines DevSecOps]()
  - [thenewstack](https://thenewstack.io/cloudbees-scales-jenkins-redefines-devsecops/)

- [ ] [The 6 Pillars of Platform Engineering: Part 1 — Security]()
  - [thenewstack](https://thenewstack.io/the-6-pillars-of-platform-engineering-part-1-security/)

- [ ] [A Guide to Open Source Platform Engineering]()
  - [thenewstack](https://thenewstack.io/a-guide-to-open-source-platform-engineering/)

- [ ] [Drive Platform Engineering Success with Humanitec and Port]()
  - [thenewstack](https://thenewstack.io/drive-platform-engineering-success-with-humanitec-and-port/)

- [ ] [Demo: Building an Internal Developer Portal with Port]()
  - [thenewstack](https://thenewstack.io/demo-building-an-internal-developer-portal-with-port/)

- [ ] [Platform Engineering: What’s Hype and What’s Not?]()
  - [thenewstack](https://thenewstack.io/platform-engineering-whats-hype-and-whats-not/)

- [ ] [How to Create an Internal Developer Portal MVP]()
  - [thenewstack](https://thenewstack.io/how-to-create-an-internal-developer-portal-mvp/)

- [ ] [Next-Gen Observability: Monitoring and Analytics in Platform Engineering]()
  - [thenewstack](https://thenewstack.io/next-gen-observability-monitoring-and-analytics-in-platform-engineering/)

- [ ] [Platform Engineering Demands a Product Mindset]()
  - [thenewstack](https://thenewstack.io/platform-engineering-demands-a-product-mindset/)

- [ ] [How Platform Engineering Can Help Keep Cloud Costs in Check]()
  - [thenewstack](https://thenewstack.io/how-platform-engineering-can-help-keep-cloud-costs-in-check/)

- [ ] [7 Benefits of Developer Access to Production ]()
  - [thenewstack](https://thenewstack.io/7-benefits-of-developer-access-to-production/)

- [ ] [How to Pave Golden Paths That Actually Go Somewhere]()
  - [thenewstack](https://thenewstack.io/how-to-pave-golden-paths-that-actually-go-somewhere/)

- [ ] [Streamline Platform Engineering with Kubernetes]()
  - [thenewstack](https://thenewstack.io/streamline-platform-engineering-with-kubernetes/)

- [ ] [Backstage in Production: Considerations for Platform Teams]()
  - [thenewstack](https://thenewstack.io/backstage-in-production-considerations-for-platform-teams/)

- [ ] [How Spotify Achieved a Voluntary 99% Internal Platform Adoption Rate]()
  - [thenewstack](https://thenewstack.io/how-spotify-achieved-a-voluntary-99-internal-platform-adoption-rate/)

- [ ] [SRE vs Platform Engineer: Can’t We All Just Get Along?]()
  - [thenewstack](https://thenewstack.io/sre-vs-platform-engineer-cant-we-all-just-get-along/)

- [ ] [IDPs: A Piece of the Developer Experience Puzzle]()
  - [thenewstack](https://thenewstack.io/idps-a-piece-of-the-developer-experience-puzzle/)

- [ ] [New Ebook: Get Our Free Platform Engineering Guide]()
  - [thenewstack](https://thenewstack.io/new-ebook-free-platform-engineering-guide/)

- [ ] [The Game-Changing Impact of Automation on Team Dynamics]()
  - [thenewstack](https://thenewstack.io/the-game-changing-impact-of-automation-on-team-dynamics/)

- [ ] [Cloud Portability: How Platform Engineering Pushes Past Toil]()
  - [thenewstack](https://thenewstack.io/cloud-portability-how-platform-engineering-pushes-past-toil/)

- [ ] [The Real Business Value of Platform Engineering]()
  - [thenewstack](https://thenewstack.io/the-real-business-value-of-platform-engineering/)

- [ ] [Documentation Is More than Your Thinnest Viable Platform]()
  - [thenewstack](https://thenewstack.io/documentation-is-more-than-your-thinnest-viable-platform/)

- [ ] [Shaping DevOps with the Best of ‘By Audit’ and ‘By Design’]()
  - [thenewstack](https://thenewstack.io/shaping-devops-with-the-best-of-by-audit-and-by-design/)

- [ ] [Use Your Internal Developer Portal to Drive Better AppSec]()
  - [thenewstack](https://thenewstack.io/use-your-internal-developer-portal-to-drive-better-appsec/)

- [x] [VMware Expands Tanzu into a Full Platform Engineering Environment]()
  - [thenewstack](https://thenewstack.io/vmware-expands-tanzu-into-a-full-platform-engineering-environment/)

## 2023-06

- [x] [At PlatformCon: For Realtor.com, Success Is Driven by Stories](https://github.com/shinyay/doc-to-read/files/11766045/2023-06-13_At.PlatformCon_.For.Realtor.com.Success.Is.Driven.by.Stories.-.The.New.Stack.pdf)
  - [thenewstack](https://thenewstack.io/at-platformcon-for-realtor-com-success-is-driven-by-stories/)

- [x] [‘Running Service’ Blueprint for a Kubernetes Developer Portal](https://github.com/shinyay/doc-to-read/files/11684769/2023-06-07_.Running.Service.Blueprint.for.a.Kubernetes.Developer.Portal.-.The.New.Stack.pdf)
  - [thenewstack](https://thenewstack.io/running-service-blueprint-for-a-kubernetes-developer-portal/)

- [x] [The Art of Platform Marketing: You’ve Gotta Sell It](https://github.com/shinyay/doc-to-read/files/11672874/2023-06-06_The.Art.of.Platform.Marketing_.You.ve.Gotta.Sell.It.-.The.New.Stack.pdf)

  - [thenewstack](https://thenewstack.io/the-art-of-platform-marketing-youve-gotta-sell-it/)

## 2023-05

- [x] [Could WebAssembly Be the Key to Decreasing Kubernetes Use?]()
  - [thenewstack](https://thenewstack.io/could-webassembly-be-the-key-to-decreasing-kubernetes-use/)

  > Kubernetes forces developers to care about infrastructure and they don’t necessarily want to, he added.

  > “Basically, developers have to care about their infrastructure much more than they need to,” he said. “A lot of these things around microservices, we did them in Kubernetes because that was a great way to do it before we had stuff like WebAssembly, but microservices and functions … all those things work better in a world where WebAssembly exists because you focus just on writing that code.”

- [x] [Wardley Mapping and Strategy for Software Developers]()
  - [thenewstack](https://thenewstack.io/wardley-mapping-and-strategy-for-software-developers/)

- [x] [4 Ways to Enhance Your Dockerfiles]()
  - [thenewstack](https://thenewstack.io/four-ways-to-enhance-your-dockerfiles/)

- [x] [Why Successful Platform Engineering Teams Need a Product Manager]()
  - [thenewstack](https://thenewstack.io/why-successful-platform-engineering-teams-need-a-product-manager/)

- [x] [High-Performing DevOps Teams Build Self-Service Platforms]()
  - [thenewstack](https://thenewstack.io/high-performing-devops-teams-build-self-service-platforms/)

- [x] [KubeCon Europe 2023 highlights Kubernetes explosion and need for instant platform engineering](https://github.com/shinyay/doc-to-read/files/11589323/2023-05-08_KubeCon.Europe.2023.highlights.Kubernetes.explosion.and.need.for.instant.platform.engineering._.Cloud.Native.Computing.Foundation.pdf)
  - [cncf](https://www.cncf.io/blog/2023/05/08/kubecon-europe-2023-highlights-kubernetes-explosion-and-need-for-instant-platform-engineering/)

- [x] [Software Architecture and Design InfoQ Trends Report - April 2023](https://github.com/shinyay/doc-to-read/files/11589320/2023-0407_Software.Architecture.and.Design.InfoQ.Trends.Report.-.April.2023.pdf)
  - [infoq](https://www.infoq.com/articles/architecture-trends-2023/)
  - [podcast](https://www.infoq.com/podcasts/architecture-trends-report-2023/)

- [x] [Culture & Methods Trends Report March 2023](https://github.com/shinyay/doc-to-read/files/11589324/2023-03-31_Culture.Methods.Trends.Report.March.2023.pdf)
  - [infoq](https://www.infoq.com/articles/culture-trends-2023/)
  - [podcast](https://www.infoq.com/podcasts/culture-trends-2023/)

- [x] [Solving the SBOM crisis with WebAssembly components](https://github.com/shinyay/doc-to-read/files/11589321/2023-05-10_Solving.the.SBOM.crisis.with.WebAssembly.components._.InfoWorld.pdf)
  - [infoworld](https://www.infoworld.com/article/3694902/solving-the-sbom-crisis-with-webassembly-components.html)

- [x] [7 awesome Java projects you should know about](https://github.com/shinyay/doc-to-read/files/11589322/2023-05-10_7.awesome.Java.projects.you.should.know.about._.InfoWorld.pdf)
  - [infoworld](https://www.infoworld.com/article/3694933/7-awesome-java-projects-you-should-know-about.html)

- [ ] [Can Rust Beat Javascript in 2023?](https://github.com/shinyay/doc-to-read/files/11474940/2023-04-21_Can.Rust.Beat.Javascript.in.2023_._.Rust.Web.Dev.with.Josh.Mo.pdf)

  - [blog](https://joshmo.bearblog.dev/can-rust-beat-javascript-in-2023/)

- [x] [Quarkus 3.0 Released: Improving Cloud-Native Java Development with Jakarta EE 10 Support](https://github.com/shinyay/doc-to-read/files/11459191/2023-05-09_Quarkus.3.0.Released_.Improving.Cloud-Native.Java.Development.with.Jakarta.EE.10.Support.pdf)
  - [infoq](https://www.infoq.com/news/2023/05/quarkus-improves-cloud-native)

- [x] [Platform as a Runtime (PaaR) - Beyond Platform Engineering](https://github.com/shinyay/doc-to-read/files/11459217/2023-05-02_Platform.as.a.Runtime.PaaR.-.Beyond.Platform.Engineering.pdf)
  - [blog](https://www.aviransplace.com/post/platform-as-a-runtime-paar-beyond-platform-engineering)

- [x] [Open Liberty 23.0.0.3 Unveiled: Embracing Cloud-Native Java Microservices, Jakarta EE 10 and beyond](https://github.com/shinyay/doc-to-read/files/11459192/2023-05-05_Open.Liberty.23.0.0.3.Unveiled_.Embracing.Cloud-Native.Java.Microservices.Jakarta.EE.10.and.beyond.pdf)
  - [infoq](https://www.infoq.com/news/2023/05/open-liberty-23003-unveiled/)

## 2023-04

- [x] [Why You Should Run Your Platform Team Like a Product Team](https://github.com/shinyay/doc-to-read/files/11396887/2023-04-12_Why.You.Should.Run.Your.Platform.Team.Like.a.Product.Team.-.The.New.Stack.pdf)
  - [thenewstack](https://thenewstack.io/why-you-should-run-your-platform-team-like-a-product-team/)

- [x] [KubeCon Panel: How Platform Engineering Benefits Developers](https://github.com/shinyay/doc-to-read/files/11396763/2024-04-28_KubeCon.Panel_.How.Platform.Engineering.Benefits.Developers.-.The.New.Stack.pdf)
  - [thenewstack](https://thenewstack.io/kubecon-panel-how-platform-engineering-benefits-developers/)

- [x] [KubeCon EU + CloudNativeCon 2023 Summary: DevEx, Debugging, and Doubling-down on Community](https://github.com/shinyay/doc-to-read/files/11338400/2027-04-27_KubeCon.EU.%2B.CloudNativeCon.2023.Summary._.Ambassador.Labs.pdf)
  - [medium](https://blog.getambassador.io/kubecon-eu-cloudnativecon-2023-summary-devex-debugging-and-doubling-down-on-community-82abee5853b3)

- [x] [What Is DX? (Developer Experience)](https://github.com/shinyay/doc-to-read/files/11316031/2019-10-31_What.Is.DX_.Developer.Experience._.by.Albert.Cavalcante._.The.Startup._.Medium.pdf)
  - [medium](https://medium.com/swlh/what-is-dx-developer-experience-401a0e44a9d9)

- [x] [What is Developer Experience?](https://github.com/shinyay/doc-to-read/files/11316033/2022-07-18_What.is.Developer.Experience_.-.DEV.Community.pdf)
  - [devto](https://dev.to/jacobandrewsky/what-is-developer-experience-2lh8)

- [ ] [Defining the Developer Experience]()
  - [dzone](https://dzone.com/articles/developer-experience)

- [x] [Everything You [Didn't] Want To Know About Developer Experience](https://github.com/shinyay/doc-to-read/files/11316035/2023-04-27_Everything.You.Didn.t.Want.To.Know.About.Developer.Experience.-.DEV.Community.pdf)
  - [devto](https://dev.to/rainleander/everything-you-didnt-want-to-know-about-developer-experience-1e30)

- [ ] [CNCF Platforms White Paper](https://github.com/shinyay/doc-to-read/files/11207678/platforms-def-v1.0.pdf)
  - [cncf](https://appdelivery.cncf.io/whitepapers/platforms/)

- [x] [DB Integration Tests with Spring Boot and Testcontainers](https://github.com/shinyay/doc-to-read/files/11147106/DB.Integration.Tests.with.Boot.and.Testcontainers._.Baeldung.pdf)
  - [baeldung](https://www.baeldung.com/spring-boot-testcontainers-integration-test)

## 2023-03

- [ ] [The Challenge of Cognitive Load in Platform Engineering: a Discussion with Paula Kennedy]()
  - [infoq](https://www.infoq.com/articles/cognitive-load-platform-engineering/)

- [ ] [Hard-Won Lessons from the Trenches: Failure Modes of Platform Engineering — and How to Avoid Them]()
  - [infoq](https://www.infoq.com/articles/platform-engineering-lessons-learned/)

- [x] [Green Software Development - What Can You Do Now, and Where is the Industry Heading?](https://github.com/shinyay/doc-to-read/files/11070354/2023-03-23_Green.Software.Development.-.What.Can.You.Do.Now.and.Where.is.the.Industry.Heading.pdf)
  - [infoq](https://www.infoq.com/news/2023/03/green-software-development/)

- [x] [Getting Started With CI:CD Pipeline Security](https://github.com/shinyay/doc-to-read/files/11012882/DZone.-.Getting.Started.With.CI.CD.Pipeline.Security.pdf)
  - [DZone](https://dzone-resources.dzone.com/free/w_defa3617)

- [x] [The Platform Engineering Guide: Principles and Best Practices]()
  - [InfoQ](https://www.infoq.com/minibooks/platform-engineering-guide/)

- [x] [What Is Psychological Safety?](https://github.com/shinyay/doc-to-read/files/10876806/What.Is.Psychological.Safety_.pdf)
  - [HBR](https://hbr.org/2023/02/what-is-psychological-safety)

## 2023-02

- [ ] [What Is Essentialism, and How Does It Make Software More Efficient?](https://github.com/shinyay/doc-to-read/files/10637256/What.Is.Essentialism.and.How.Does.It.Make.Software.More.Efficient.-.DZone.pdf)
  - [dzone](https://dzone.com/articles/what-is-essentialism-and-how-does-it-make-software-more-efficient)

- [ ] [How To Approach Legacy System Modernization](https://github.com/shinyay/doc-to-read/files/10637257/How.to.Approach.Legacy.System.Modernization.-.DZone.pdf)
  - [dzone](https://dzone.com/articles/how-to-approach-legacy-system-modernization)

## 2023-01

- [x] [An Overview of the Kubernetes Gateway API and Envoy Gateway](https://github.com/shinyay/doc-to-read/files/10564228/An.Overview.of.the.Kubernetes.Gateway.API.and.Envoy.Gateway._.by.Dave.Sudia._.Jan.2023._.Ambassador.Labs.pdf)
  - [Medium](https://blog.getambassador.io/an-overview-of-the-kubernetes-gateway-api-and-envoy-gateway-8162bfb7fb9e)

- [x] [JavaScript or WebAssembly: Which Is More Energy Efficient and Faster?](https://github.com/shinyay/doc-to-read/files/10541880/JavaScript.or.WebAssembly_.Which.Is.More.Energy.Efficient.and.Faster_.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/javascript-vs-wasm-which-is-more-energy-efficient-and-faster/)

- [x] [Reduce CO2 Emissions and Cost by Increasing Software Efficiency](https://github.com/shinyay/doc-to-read/files/10541879/Reduce.CO2.Emissions.and.Cost.by.Increasing.Software.Efficiency.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/reduce-co2-emissions-and-cost-by-increasing-software-efficiency/)
  > Software Efficiency
  > Improving software efficiency increases the speed and throughput that a unit of resources (a computer, VM, container or node) can handle. Therefore, an efficient software platform would require fewer units to handle a specific workload/demand. Fewer units of resources result in reduced costs and emissions. That’s a win-win situation for businesses and the planet.

- [ ] [Internal Developer Portals Can Do More than You Think](https://github.com/shinyay/doc-to-read/files/10527023/Internal.Developer.Portals.Can.Do.More.than.You.Think.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/an-inside-look-at-what-gitllabs-web-ide-offers-developers/)

- [ ] [the 2023 State of Platform Engineering Report](https://github.com/shinyay/doc-to-read/files/10515806/report-puppet-sodor-2023-platform-engineering.pdf)
  - [puppet](https://www.puppet.com/resources/state-of-platform-engineering)

- [ ] [What is platform engineering?](https://github.com/shinyay/doc-to-read/files/10515799/What.is.platform.engineering_.pdf)
  - [platformengineering](https://platformengineering.org/blog/what-is-platform-engineering)

- [ ] [What is Platform Engineering?](https://github.com/shinyay/doc-to-read/files/10515798/What.is.Platform.Engineering_.What.to.Know._.Puppet.by.Perforce.pdf)
  - [puppet](https://www.puppet.com/blog/what-platform-engineering)

- [ ] [Internal Developer Advocacy: What Should You Do Next?](https://github.com/shinyay/doc-to-read/files/10515786/Internal.Developer.Advocacy_.What.Should.You.Do.Next_.-.The.New.Stack.pdf)
  - [thenewstack](https://thenewstack.io/internal-developer-advocacy-what-should-you-do-next/)

- [ ] [Are Your “Value Streams” Keeping You Stuck in the Past?](https://github.com/shinyay/doc-to-read/files/10515778/Are.Your.Value.Streams.Keeping.You.Stuck.in.the.Past_.pdf)
  - [InfoQ](https://www.infoq.com/articles/value-streams-stuck-past/)

- [ ] [Crossplane: A Package-Based Approach to Platform Building](https://github.com/shinyay/doc-to-read/files/10515772/Crossplane_.A.Package-Based.Approach.to.Platform.Building.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/crossplane-a-package-based-approach-to-platform-building)

- [ ] [Platform Engineering Benefits Developers, and Companies too](https://github.com/shinyay/doc-to-read/files/10515750/Platform.Engineering.Benefits.Developers.and.Companies.too.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/platform-engineering-benefits-developers-and-companies-too/)

- [ ] [The Current Trends in WebAssembly](https://github.com/shinyay/doc-to-read/files/10515746/The.Current.Trends.in.WebAssembly._.by.Yiming.Cao._.Jan.2023._.Better.Programming.pdf)
  - [Blog](https://betterprogramming.pub/the-current-trends-in-webassembly-68022a8f9807)

## 2022-11

- [ ] [A Platform Team Product Manager Determines DevOps Success](https://github.com/shinyay/doc-to-read/files/10515756/A.Platform.Team.Product.Manager.Determines.DevOps.Success.-.The.New.Stack.pdf)
  - [THENEWSTACK](https://thenewstack.io/a-platform-team-product-manager-determines-devops-success/)

- [x] [This Week in Spring - November 15th, 2022](https://github.com/shinyay/doc-to-read/files/10026617/This.Week.in.Spring.-.November.15th.2022.pdf)
  - [SpringBlog](https://spring.io/blog/2022/11/15/this-week-in-spring-november-15th-2022)

- [x] [Spring Framework 6.0.0-RC4 available now](https://github.com/shinyay/doc-to-read/files/10026613/Spring.Framework.6.0.0-RC4.available.now.pdf)
  - [SpringBlog](https://spring.io/blog/2022/11/09/spring-framework-6-0-0-rc4-available-now)

- [x] [Spring Cloud 2021.0.5 (codename Jubilee) Has Been Released](https://github.com/shinyay/doc-to-read/files/10026599/Spring.Cloud.2021.0.5.codename.Jubilee.Has.Been.Released.pdf)
  - [SpringBlog](https://spring.io/blog/2022/11/08/spring-cloud-2021-0-5-codename-jubilee-has-been-released)

- [x] [Spring Modulith 0.1 M2 released](https://github.com/shinyay/doc-to-read/files/10026591/Spring.Modulith.0.1.M2.released.pdf)
  - [SpringBlog](https://spring.io/blog/2022/11/02/spring-modulith-0-1-m2-released)

- [x] [This Week in Spring - November 8th, 2022](https://github.com/shinyay/doc-to-read/files/10026579/This.Week.in.Spring.-.November.8th.2022.pdf)
  - [SpringBlog](https://spring.io/blog/2022/11/08/this-week-in-spring-november-8th-2022)

- [x] [Why Wasm is the future of cloud computing](https://github.com/shinyay/doc-to-read/files/9976779/Why.Wasm.is.the.future.of.cloud.computing._.InfoWorld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3678208/why-wasm-is-the-future-of-cloud-computing.html)

## 2022-10

- [x] [The ever-widening world of Wasm](https://github.com/shinyay/doc-to-read/files/9721083/2022-09-27-infoworld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3674124/the-ever-widening-world-of-wasm.html)
  > The World Wide Web Consortium (W3C) first announced Wasm, i.e., WebAssembly, back in 2015 and published it in 2018. Originally designed solely for use in the browser, the in-the-weeds Wasm is garnering interest as a potential barrier breaker across different hardware and software environments. The original vision for Wasm was a security tool that allowed developers to safely use compiled languages like C, C++, or Rust in the browser, while at the same time preventing the code from taking over a user’s machine.
  > Wasm blockers: Perhaps a bigger issue is that Wasm, a very specific instruction set architecture, is not currently POSIX-compliant, so you can’t use it to do a lot of standard things developers have come to expect (think of things like opening a file or a network socket).

## 2022-09

- [x] [Resilient Organizations Make Psychological Safety a Strategic Priority](https://github.com/shinyay/doc-to-read/files/9643085/Resilient.Organizations.Make.Psychological.Safety.a.Strategic.Priority.pdf)
  - [HBR](https://hbr.org/2022/08/resilient-organizations-make-psychological-safety-a-strategic-priority)
  > 3 cultural dimensions are critical for resilience:
  > ✅Integrity: Ethical leadership and courageous candor
  > ✅Innovation: Fearless collaboration
  > ✅Inclusion:  Respect and belonging
- [ ] [4 Steps to Boost Psychological Safety at Your Workplace](https://github.com/shinyay/doc-to-read/files/9643094/4.Steps.to.Boost.Psychological.Safety.at.Your.Workplace.pdf)
  - [HBR](https://hbr.org/2021/06/4-steps-to-boost-psychological-safety-at-your-workplace)

## 2022-08

- [ ] [Data Oriented Programming in Java](https://github.com/shinyay/doc-to-read/files/9390546/2022-06-20-infoq.pdf)
  - [InfoQ](https://www.infoq.com/articles/data-oriented-programming-java/)

- [ ] [How to Optimize Java Apps on Kubernetes](https://github.com/shinyay/doc-to-read/files/9389162/2022-07-22-thenewstack.pdf)
  - [TheNewStack](https://thenewstack.io/how-to-optimize-java-apps-on-kubernetes/)

- [ ] [Reduce Carbon Dioxide Emissions with Serverless and Kubernetes Native Java](https://github.com/shinyay/doc-to-read/files/9378896/2022-06-15-infoq.pdf)
  - [InfoQ](https://www.infoq.com/articles/reduce-CO2-with-serveless/)

- [x] [SBOMs Are Great for Supply Chain Security but Buyers Beware](https://github.com/shinyay/doc-to-read/files/9335137/2022-08-09-thenewstack.pdf)
  - [TheNewStack](https://thenewstack.io/sboms-are-great-for-supply-chain-security-but-buyers-beware/)

- [ ] [Is Kubernetes the Next Fault Domain?](https://github.com/shinyay/doc-to-read/files/9334421/2022-08-12-thenewstack.pdf)
  - [TheNewStack](https://thenewstack.io/is-kubernetes-the-next-fault-domain/)

- [ ] [The Need for a Kubernetes Alternative](https://github.com/shinyay/doc-to-read/files/9332183/2022-08-01-DZone.pdf)
  - [DZone](https://dzone.com/articles/the-need-for-a-kubernetes-alternative)

- [ ] [7 reasons to embrace Web3 — and 7 reasons not to](https://github.com/shinyay/doc-to-read/files/9332179/2022-03-07-infoworld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3651494/7-reasons-to-embrace-web3-and-7-reasons-not-to.html)

- [ ] [When Microservices Are a Bad Idea](https://github.com/shinyay/doc-to-read/files/9332175/2022-08-05-dzone.pdf)
  - [DZone](https://dzone.com/articles/when-microservices-are-a-bad-idea)

- [ ] [When Wasm and Docker Work (and Do Not Work) Together](https://github.com/shinyay/doc-to-read/files/9296831/2022-08-08-thenewstack.pdf)
  - [TheNewStack](https://thenewstack.io/when-wasm-and-docker-work-and-do-not-work-together/)

- [ ] [Unblocked by Design](https://github.com/shinyay/doc-to-read/files/9278864/2022-0805-thenewstack.pdf)
  - [InfoQ](https://www.infoq.com/presentations/problems-async-arch/)

- [ ] [All the Things a Service Mesh Can Do](https://github.com/shinyay/doc-to-read/files/9278864/2022-0805-thenewstack.pdf)
  - [TheNewStack](https://thenewstack.io/all-the-things-a-service-mesh-can-do/)

- [ ] [Developer Satisfaction Is Key to Engineering Success](https://github.com/shinyay/doc-to-read/files/9278837/2022-07-26-infoq.pdf)
  - [Infoq](https://www.infoq.com/podcasts/engineering-success-key/)

- [ ] [API Gateway Vs. Service Mesh: What’s the Difference?](https://github.com/shinyay/doc-to-read/files/9238847/2022-08-01-devops.pdf)
  - [DevOps](https://devops.com/api-gateway-vs-service-mesh-whats-the-difference/)

## 2022-07

- [x] [7 reasons Java is still great](https://github.com/shinyay/doc-to-read/files/9238834/2022-07-18-InfoWorld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3666525/7-reasons-java-is-still-great.html)

- [ ] [Cloud complicates development, but GraphQL and supergraphs offer hope]((https://github.com/shinyay/doc-to-read/files/9238781/2022-06-22-infoworld.pdf))
  - [InfoWorld](https://www.infoworld.com/article/3662752/cloud-complicates-development-but-graphql-and-supergraphs-offer-hope.html)

- [ ] [Using Multiple Azure Storage Accounts From a Single Spring Boot App](https://github.com/shinyay/doc-to-read/files/9193061/2022-07-25-dzone.pdf)
  - [DZone](https://dzone.com/articles/using-multiple-azure-storage-accounts-from-a-single-spring-boot-app)

- [ ] [Spring Boot 2.7 Release Notes - Upgrading from Spring Boot 2.6](https://github.com/shinyay/doc-to-read/files/9188893/2022-07-26-github.pdf)
  - [GitHub](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.7-Release-Notes)

- [ ] [What's New In TAP 1.2](https://github.com/shinyay/doc-to-read/files/9178239/2022-07-14-b
log.pdf)
  - [Blog](https://www.vrabbi.cloud/post/tap-1-2-is-ga)

- [x] [DevOps and Cloud InfoQ Trends Report – June 2022](https://github.com/shinyay/doc-to-read/files/9178216/2022-06-21-InfoQ.pdf)
  - [InfoQ](https://www.infoq.com/articles/devops-and-cloud-trends-2022/)

- [x] [Software Architecture: It Might Not Be What You Think It Is](https://github.com/shinyay/doc-to-read/files/9178180/2022-04-15-infoq.pdf)
  - [InfoQ](https://www.infoq.com/articles/what-software-architecture/)

- [x] [Getting Started With RSocket Kotlin](https://github.com/shinyay/doc-to-read/files/9178169/2022-06-25-dzone.pdf)
  - [DZone](https://dzone.com/articles/getting-started-with-rsocket-kotlin)

## 2022-06

- [x] [The experience of working in Developer Experience](https://github.com/shinyay/doc-to-read/files/8955391/2022-04-04-medium.pdf)
  - [medeium](https://medium.com/clarityai-engineering/the-experience-of-working-in-developer-experience-c51dfae1a973)

- [x] [KubeCon EU 2022 Summary: Cloud Novices, Golden Paths, and Software Supply Chains](https://blog.getambassador.io/kubecon-eu-2022-summary-cloud-novices-golden-paths-and-software-supply-chains-f38d34b0c5a4)

## 2022-05

- [ ] [What Is Zero Trust Network Access (ZTNA)?](https://github.com/shinyay/doc-to-read/files/8628303/2022-05-03-thenewstack.pdf)
  - [thenewstack](https://thenewstack.io/what-is-zero-trust-network-access-ztna)

- [x] [What Is Zero Trust Security?](https://github.com/shinyay/doc-to-read/files/8628297/2022-03-30-thenewstack.pdf)
  - [thenewstack](https://thenewstack.io/what-is-zero-trust-security/)

  >Zero Trust is built on a couple of principles:
  >  - Always verify access for all users across all devices.
  >  - By minimizing access, the impact of external and internal breaches is also minimized if they do occur.
  >  - Access to resources, systems, software, and applications is determined by the policy and user identification only.
  >  - Implementing contextual analysis and collection can help you see behavior patterns across the network and respond quickly.

  >With zero trust implemented, companies can accomplish the following:
  > - Improve real-time visibility into all their cloud, hybrid, and on-premise environments.
  > - Protect data, applications, devices, and networks from cyberattack infiltration.
  > - Minimize the risk of data and security breaches.
  > - Decrease the time it takes to detect and respond to an attack.
  > - Continuously monitor components, users, workloads, and devices across multiple environments.
  > - Build a consistent user experience for internal and external employees and contractors.

## 2022-04

- [ ] [Innovation Insight for SBOMs](https://github.com/shinyay/doc-to-read/files/8535120/2022-02-14-gartner.pdf)
  - [gartner](https://www.gartner.com/doc/reprints?id=1-29K601XV&ct=220331&st=sb)

- [ ] [Service Mesh Ultimate Guide 2020: Managing Service-to-Service Communications](https://github.com/shinyay/doc-to-read/files/8492358/2020-02-18-infoq.pdf)
  - [infoq](https://www.infoq.com/articles/service-mesh-ultimate-guide/)

- [ ] [Securing the Kubernetes software supply chain](https://github.com/shinyay/doc-to-read/files/8492376/2021-12-15-InfoWorld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3644808/securing-the-kubernetes-software-supply-chain.html)

## 2022-03

- [ ] [Cloud-Native Is about Culture, Not Containers](https://github.com/shinyay/doc-to-read/files/8231103/2021-03-17-infoq.pdf)
  - [infoq](https://www.infoq.com/articles/cloud-native-culture)

- [x] [EJB History](https://github.com/shinyay/doc-to-read/files/8308902/2011-05-28-blog.pdf)
  - [blog](https://ryoasai.hatenadiary.org/entry/20110528/1306594182)

- [x] [Build a software bill of materials (SBOM) for open source supply chain security](https://github.com/shinyay/doc-to-read/files/8258657/2022-03-14-snyk.pdf)
  - [snyk](https://snyk.io/blog/building-sbom-open-source-supply-chain-security/)

- [x] [The future of Kubernetes – and why developers should look beyond Kubernetes in 2022](https://github.com/shinyay/doc-to-read/files/8250808/2022-02-22-blog.pdf)
  - [blog](https://www.eficode.com/blog/the-future-of-kubernetes-and-why-developers-should-look-beyond-kubernetes-in-2022)

  > - The future of Kubernetes is in the custom resource definitions (CRDs) and abstractions which we build on top of Kubernetes and make available to users through CRDs.

## 2022-02

- [x] [More Secure Open Source Software: A Shared Responsibility](https://github.com/shinyay/doc-to-read/files/8150500/2022-01-19-vmware.pdf)
  - [vmware](https://news.vmware.com/company/secure-open-source-software-a-shared-responsibility)

  > - Open Source Artifact Creation
  > - Code Quality Checks and Balances
  > - Community Engagement Incentives
  > - Software Supply Chain Agility Incentives
  > - Public-Private Collaboration and Threat Information Sharing

- [x] [Strength in Numbers: The White House Open Source Security Summit](https://github.com/shinyay/doc-to-read/files/8150491/2022-01-18-vmware.pdf)
  - [vmware](https://octo.vmware.com/strength-in-numbers-the-white-house-open-source-security-summit/)

  > - [Readout of White House Meeting on Software Security](https://www.whitehouse.gov/briefing-room/statements-releases/2022/01/13/readout-of-white-house-meeting-on-software-security/)

- [x] [Kubernetes and the Next Generation of PaaS](https://github.com/shinyay/doc-to-read/files/8138869/2022-02-09-thenewstack.pdf)
  - [thenewstack](https://thenewstack.io/kubernetes-and-the-next-generation-of-paas/)
  > - Easy as PaaS for developers
  > - No vendor lock-in
  > - Full Kubernetes power

- [x] [「金融分野におけるサイバーセキュリティ強化に向けた取組方針」のアップデートについて(Ver. 3.0)](https://www.fsa.go.jp/news/r3/cyber/cyber-summary.pdf)
  - [Cyber Policy](https://github.com/shinyay/doc-to-read/files/8108539/cyber-policy.pdf)
  - [金融庁](https://www.fsa.go.jp/news/r3/cyber/torikumi2022.html)

- [x] [The Linux Foundation Releases The State of Software Bill of Materials (SBOM) and Cybersecurity Readiness Research](https://github.com/shinyay/doc-to-read/files/8088877/2022-02-01-lf.pdf)
  - [lf](https://www.linuxfoundation.org/press-release/the-linux-foundation-releases-the-state-of-software-bill-of-materials-sbom-and-cybersecurity-readiness-research/)
  - [The State of Software Bill of Materials and Cybersecurity Readiness report](https://github.com/shinyay/doc-to-read/files/8088880/LFResearch_SBOM_Report_020422.pdf)
  - [Infographic](https://github.com/shinyay/doc-to-read/files/8088879/LFResearch_SBOM_Infographic-1.pdf)

  > What is an SBOM
  > An SBOM is formal and machine-readable metadata that uniquely identifies a software package and its contents.
  > It may include other information about its contents, including copyrights and license data.

- [x] [SOFTWARE BILL OF MATERIALS](https://www.cisa.gov/sbom)

- [x] [CISA SBOM-A-RAMA](https://www.cisa.gov/cisa-sbom-rama)
  - [CISA SBOM-a-rama Day 1](https://youtu.be/aKEpHMVusjM)
  - [CISA SBOM-a-rama Day 2](https://youtu.be/6puCkTj0qcE)

- [x] [Security: The Value of SBOMs](https://github.com/shinyay/doc-to-read/files/8057219/2022-02-07-blog.pdf)
  - [blog](https://fluxcd.io/blog/2022/02/security-the-value-of-sboms/)

  > - Big organizations, corporate or governmental, already keep track of SBOMs and make decisions based on the information provided there. Some started requiring SBOMs for software in-use. A good example of this is the government of the USA requiring SBOM from software suppliers.
  > - [Executive Order on Improving the Nation’s Cybersecurity](https://www.whitehouse.gov/briefing-room/presidential-actions/2021/05/12/executive-order-on-improving-the-nations-cybersecurity/)

  > - Possible use-cases for SBOMs
  > - Security alerts of dependencies will be the most obvious use-case. If a CVE is detected, you can inspect your SBOM and see if the components you are using are in any way affected
  > - It will be easy to identify when a certain component was created and how. In addition to that, having the licensing information of all the pieces, you better know what you can do with it (redistribute, change, etc)
  > - Automation allows you to send alerts, if a compliance issue is detected, e.g. if the licensing of updated/replaced dependencies changes
  > Missing components or required build files. Incompatible licenses and more

- [x] [The History of Pets vs Cattle and How to Use the Analogy Properly](https://github.com/shinyay/doc-to-read/files/8021890/2016-09-29-blog.pdf)
  - [blog](http://cloudscaling.com/blog/cloud-computing/the-history-of-pets-vs-cattle)

  > - “scale-up” vs. “scale-out” architectures
  > - pets vs cattle in the context of cloud, and emphasizing the disposability of cattle and the uniqueness of pets
  > - Pets: Servers or server pairs that are treated as indispensable or unique systems that can never be down. Typically they are manually built, managed, and “hand fed”. Examples include mainframes, solitary servers, HA loadbalancers/firewalls (active/active or active/passive), database systems designed as master/slave (active/passive), and so on.
  > - Cattle: Arrays of more than two servers, that are built using automated tools, and are designed for failure, where no one, two, or even three servers are irreplaceable. Typically, during failure events no human intervention is required as the array exhibits attributes of “routing around failures” by restarting failed servers or replicating data through strategies like triple replication or erasure coding. Examples include web server arrays, multi-master datastores such as Cassandra clusters, multiple racks of gear put together in clusters, and just about anything that is load-balanced and multi-master.

- [x] [App Modernization: 5 Tips When Migrating to Kubernetes](https://github.com/shinyay/doc-to-read/files/8000832/2022-01-27-thenewstack.pdf)
  - [thenewstack](https://thenewstack.io/app-modernization-5-tips-when-migrating-to-kubernetes)

  > 1. Treat Your Legacy Apps Like Pets, Not Cattle
  > - Pets are each vitally important, but Cattle are interchangeable.
  > - In the context of a cloud migration, infrastructure managers need to apply this adage in the reverse: Your apps and virtual machines should indeed be treated like pets, not like cattle.

  > 2. Don’t Just Lift and Shift — Evolve Your Approach for a Better App
  > - You could simply translate your legacy apps to a cloud-based environment. But what worked on-premises isn’t going to necessarily work in the cloud.
  > - Decomposing apps: for greater scalability, availability and flexibility
  > - Automated infrastructure: rapid releases and continuous improvement
  > - Leveraging containers rather than VMs: agility and high availablity

  > 3. But If You’re Not Ready to Leave Your VMs Behind, There Are Options
  > - Hosting your VM in the cloud, in their original on-premises format and managed by the same hypervisor,
  > - can be beneficial if there’s a lot of institutional knowledge at your organization related to their use
  > - you don’t want to give that knowledge up to learn a new system

## 2022-01

- [ ] [Kubernetes Infrastructure: Know the Inner Dev Loop](https://github.com/shinyay/doc-to-read/files/7955034/2021-03-09-thenewstack.pdf)
  - [thenewstack](https://thenewstack.io/kubernetes-infrastructure-know-the-inner-dev-loop/)

- [ ] [Tanzu Application Platform v1.0](https://github.com/shinyay/doc-to-read/files/7939508/tapv1.0.pdf)

- [ ] [PodSecurityPolicy Deprecation: Past, Present, and Future](https://github.com/shinyay/doc-to-read/files/7955047/2021-04-06-kubernetes.pdf)
  - [kubernetes](https://kubernetes.io/blog/2021/04/06/podsecuritypolicy-deprecation-past-present-and-future/)

- [ ] [Guide To GitOps](https://github.com/shinyay/doc-to-read/files/7955066/2022-01-24-weave.pdf)
  - [weaveworks](https://www.weave.works/technologies/gitops/)

- [ ] [What Is GitOps](https://github.com/shinyay/doc-to-read/files/7955049/2021-06-15-weave.pdf)
  - [weaveworks](https://www.weave.works/blog/what-is-gitops-really)

- [ ] [VMware Multi-Cloud Architecture: Enabling Choice and Flexibility](https://github.com/shinyay/doc-to-read/files/7955064/2022-01-20-vmware.pdf)
  - [vmware](https://www.vmware.com/learn/693160_REG.html)

- [ ] [VMware Project Cascade: The Future of VMware](https://github.com/shinyay/doc-to-read/files/7955055/2021-10-18-blog.pdf)
  - [blog](https://pivotnine.com/2021/10/18/vmware-project-cascade-the-future-of-vmware/)

- [ ] [DevOps tech: Shifting left on security](https://github.com/shinyay/doc-to-read/files/7955063/2022-01-19-google.pdf)
  - [google](https://cloud.google.com/architecture/devops/devops-tech-shifting-left-on-security)

- [ ] [Shifting left on security](https://cloud.google.com/files/shifting-left-on-security.pdf)

- [ ] [Kubernetes needs a developer platform](https://github.com/shinyay/doc-to-read/files/7955060/2022-01-04-blog.pdf)
  - [blog](https://odedia.org/kubernetes-needs-a-developer-platform)

- [x] [2021 Global DevSecOps Survey](https://about.gitlab.com/images/developer-survey/gitlab-devsecops-2021-survey-results.pdf)
  - [gitlab](https://about.gitlab.com/developer-survey/)

  > A full 72% of security pros rated their organizations’ security efforts as either “strong” or “good.”

  > The shift left continues: DevSecOps teams are running more DAST, SAST, container, and dependency scans than ever before.

- [ ] [DoD Enterprise DevSecOps Documents](https://software.af.mil/dsop/documents/)

- [x] [What Is DevOps? A Comprehensive Introduction](https://github.com/shinyay/doc-to-read/files/7955048/2021-04-16-bmc.pdf)
  - [bmc](https://www.bmc.com/blogs/devops-basics-introduction/)

- [x] [SRE vs DevOps: What’s The Difference?](https://github.com/shinyay/doc-to-read/files/7955053/2021-08-26-bmc.pdf)
  - [bmc](https://www.bmc.com/blogs/sre-vs-devops/)
> SRE and DevOps are often referred as two sides of the same coin, with SRE tooling and techniques complementing DevOps philosophies and practices.

> - Disaster response
> - Capacity planning
> - Monitoring

- [x] [Accelerate State of DevOps Report: The Move to Multi-Cloud](https://github.com/shinyay/doc-to-read/files/7955054/2021-09-21-devops.pdf)
  - [devops](https://devops.com/accelerate-state-of-devops-report-the-move-to-multi-cloud/)

  > - [2021 Accelerate State of DevOps Report](https://cloud.google.com/devops/state-of-devops/)
  > - [pdf](https://github.com/shinyay/doc-to-read/files/7955067/state-of-devops-2021.pdf)

  > - 973x :more frequent code deployments
  > - 6570x:faster lead time from commit to deploy
  > - 3x   :lower change failure rate (changes are 1/3 less likely to fail)
  > - 6570x:faster time to recover from incidents

- [x] [VMware eases app modernization with official launch of Tanzu Application Platform](https://github.com/shinyay/doc-to-read/files/7955062/2022-01-11-silicon.pdf)
  - [silicon](https://siliconangle.com/2022/01/11/vmware-eases-app-modernization-official-launch-tanzu-application-platform/)

- [x] [VMware Tanzu Targets Skills Gap, Shifts Security Left](https://github.com/shinyay/doc-to-read/files/7955061/2022-01-11-sdx.pdf)
  - [sdx](https://www.sdxcentral.com/articles/news/vmware-tanzu-targets-skills-gap-shifts-security-left/2022/01/)

> Kubernetes is not a developer platform

> As we talked to many enterprise customers, there has been a clear [developer experience] gap

> Tanzu Application Platform aims to minimize the challenge of navigating Kubernetes to boost developer productivity.

- [x] [Why Software Is Eating The World](https://github.com/shinyay/doc-to-read/files/7955045/2011-08-20-wsj.pdf)
  - [WSJ](https://www.wsj.com/articles/SB10001424053111903480904576512250915629460)

- [x] [Software is Eating the World, Revisited](https://github.com/shinyay/doc-to-read/files/7955050/2021-08-09-blog.pdf)
  - [Blog](https://eriktorenberg.substack.com/p/software-is-eating-the-world-revisited)

- [x] [Reflecting on Marc Andreessen’s ‘Software is Eating the World’](https://github.com/shinyay/doc-to-read/files/7955052/2021-08-20-blog.pdf)
  - [Blog](https://blogs.cisco.com/developer/softwareeatingworld01)

- [x] [Software is still eating the world](https://github.com/shinyay/doc-to-read/files/7955046/2016-06-08-tc.pdf)
  - [tc](https://techcrunch.com/2016/06/07/software-is-eating-the-world-5-years-later/)

<details>
<summary>TL;DR</summary>

> Today, the idea that “every company needs to become a software company” is considered almost a cliché.

> “Six decades into the computer revolution, four decades since the invention of the microprocessor, and two decades into the rise of the modern Internet, all of the technology required to transform industries through software finally works and can be widely delivered at global scale.”

> For a traditional industrial or service company, making the transition to acting like a software company is a massive undertaking. You need to hire new people in every part of your organization; restructure around different economics; overhaul infrastructure.

> Focus on your core
> As Steve Jobs once famously said, “Deciding what not to do is just as important as deciding what to do.”
> Uber doesn’t own their cars. They also don’t directly employ their own drivers.
> The core application and ecosystem around the Uber experience is their primary asset and differentiator.

> Focusing on your core when it comes to technology makes it easier to focus on your end-customer experience — and that’s what makes a great software company.

</details>

- [x] [What don't people understand about DevOps (yet)?](https://www.protocol.com/braintrust/what-people-misunderstand-about-devops)

<details>
<summary>TL;DR</summary>

> Companies that understand DevOps tend not to use the term “DevOps” at all, nor do they have any "DevOps engineers”.

> DevOps isn't a role. It's a culture.

> Companies that genuinely understand DevOps understand it's not a siloed team or function, but instead a new way of doing business that brings with it a new culture, new processes, embedded SREs, a hyper-focus on automation across the board, a service-based architecture, specific SLOs and an associated budget.

> DevOps shouldn't be one person's concern. It should be an integrated part of your engineering culture to have the most significant impact.

> DevOps isn't just about the speed and agility of software development and delivery. It's also about good security practices.
As DevOps practices improve, DevSecOps naturally follows.

> It is possible to achieve speed without sacrificing security. It starts by rethinking how security fits into your delivery workflow.

> The more security is woven into the best practices of everyone’s job, the easier it is to maintain your desired deployment velocity as well as ensure solid security practices. DevOps helps achieve the balance.

> I often hear people say they want a product for DevOps. But is it possible to achieve consistent DevOps with just a product?
Software development in organizations consists of a variety of requirements. Therefore, a DevOps approach that is adapted to each company is necessary.

> It is a mistake to think that you can just buy a certain technology and immediately achieve DevOps. DevOps is first and foremost a culture and a way of working. Organizations need to move from a tool-first mindset to a team-first mindset.

</details>

- [x] [Securing the Kubernetes software supply chain](https://github.com/shinyay/doc-to-read/files/7955059/2021-12-15-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3644808/securing-the-kubernetes-software-supply-chain.html)

- [x] [What is cloud-native? The modern way to develop software](https://github.com/shinyay/doc-to-read/files/7955051/2021-08-17-infoworld.pdf)
  - [InforWorld](https://www.infoworld.com/article/3281046/what-is-cloud-native-the-modern-way-to-develop-software.html)

  <details>
  <summary>TL;DR</summary>

  > Cloud-native is a modern approach to building and running software applications that exploits the flexibility, scalability, and resilience of cloud computing.

  > The Cloud Native Computing Foundation (CNCF) defines cloud-native a little more narrowly, focusing on application containerization

  > 1. The application definition and development layer
  > - The top layer of the cloud-native stack focuses on the tools used by developers to build applications

  > 2. The provisioning layer
  > - The provisioning layer of the cloud-native stack includes anything required to build and secure the environment where an application will run, ideally in a repeatable fashion

  > 3. The runtime layer
  > -  The runtime layer concerns anything associated with the running of a cloud-native application

  > 4. The orchestration and management layer
  > - The orchestration and management layer brings together the tools required to deploy, manage, and scale containerized applications, including orchestration and scheduling

  > (v.) Observability

  > Key differences between Clound Native apps and traditional apps
  > - Updatability
  > - Elasticity
  > - Mulititenancy
  > - Downtime
  > - Automation
  > - Stateless

  </details>

## 2021-12

- [x] [App Modernization: Why ‘Lift and Shift’ Isn’t Good Enough](https://github.com/shinyay/doc-to-read/files/7955058/2021-12-08-thenewstack.pdf)
  - [The New Stack](https://thenewstack.io/app-modernization-why-lift-and-shift-isnt-good-enough/)
  > For instance, less than half of participants in a 2020 survey by Harvard Business Review said their cloud strategy has been effective in terms of IT management, customer experience, and innovation. That failure rate is because many IT organizations just lift and shift — simply re-host to the cloud — to meet artificial deadlines.

  <details>
  <summary> 7Rs </summary>

  > 1. Retain
  >  - There will be data that can’t be moved, or mainframe modernization that can be postponed.

  > 2. Re-host.
  > - Move the workload from a virtual machine (VM) to a public cloud. In these cases, lift-and-shift is actually the right fit, especially if on-premise has become too costly.

  > 3. Refactor.
  > - Change the application’s code without changing its behavior, so there’s no change in user experience, but speed or efficiency should improve.

  > 4. Re-architect.
  > - Modify the source code, which often means radically changing architecture to microservices. This usually allows it to use the cloud and improve scalability.

  > 5. Rebuild.
  > - Totally rebuild in a cloud native way.

  > 6. Replace.
  > - Move to an off-the-shelf software-as-a-service product (SaaS).

  > 7. Retire.
  > - Deprecate the application.
  </details>

  > app modernization is a journey, not a destination.


- [x] [When to Choose Cloud Foundry over Kubernetes](https://github.com/shinyay/doc-to-read/files/7955057/2021-12-02-thenewstack.pdf)
  - [The New Stack](https://thenewstack.io/when-to-choose-cloud-foundry-over-kubernetes/)
  > While a single Kubernetes cluster might be easier to operate than a single Cloud Foundry, managing 100 Kubernetes clusters is several orders of magnitude harder than managing a single Cloud Foundry.

  > Managing a large number of Kubernetes clusters creates complexity that is not necessary with Cloud Foundry.

  >Kubernetes can be customized much more than Cloud Foundry and therefore accept workloads that Cloud Foundry couldn’t.

- [x] [Complexity is killing software developers](https://github.com/shinyay/doc-to-read/files/7955056/2021-11-01-infoworld.pdf)
  - [InfoWorld](https://www.infoworld.com/article/3639050/complexity-is-killing-software-developers.html)

<details>
<summary>TL;DR</summary>

> Cloud Native Application marks a clear jump in the level of complexity of our software.

  > Amazon CTO Werner Vogels said during the AWS Summit in 2019. “Was it easier in the days when everything was in a monolith? Yes, for some parts definitely.”

  > Essential is the complexity in the business domain you are working in, the fact that enterprises are extremely complicated environments, so the problems they are trying to solve are inherently complex. The other area is accidental; this is the complexity that comes with our tooling and what we layer on top when solving a problem.

  > The cloud-native era has ushered in the potential for more accidental complexity than ever before

  > The complexity inherent to a huge catalog of available services can become, in certain settings, less a strength than a liability.

  > The key to a good internal developer platform then is finding that balance between self-service for developers who want to get on with the job at hand and abstracting the tasks that are the least valuable, without making developers feel restricted

  > The idea behind having golden paths is not to limit or stifle engineers, or set standards for the sake of it. With golden paths in place, teams don’t have to reinvent the wheel, have fewer decisions to make, and can use their productivity and creativity for higher objectives. They can get back to moving fast

  > Complexity is less the issue than inconsistency in an environment by Craig McLuckie

</details>

## Author

[shinyay](https://github.com/shinyay)

- twitter: <https://twitter.com/yanashin18618>
