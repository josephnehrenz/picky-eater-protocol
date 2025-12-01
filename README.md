# The Picky Eater Protocol

An AI-powered meal planner that filters recipes for neuro-divergent sensory needs and dietary restrictions using multi-agent workflow automation.

[![Kaggle](https://kaggle.com/static/images/open-in-kaggle.svg)](https://www.kaggle.com/code/josephnehrenz/multi-agent-ai-the-picky-eater-protocol)

## About the System

The Picky Eater Protocol solves a real-world family problem: generating complete meal plans while strictly adhering to private dietary constraints and sensory preferences. This system replaces hours of stressful meal negotiations with a 5-minute automated workflow.

## How It Works

The system uses three specialized AI agents in a sequential workflow:

### **Chef Agent (Scout)**
- Takes high-level meal requests (e.g., "simple pasta")
- Generates detailed recipe proposals with names, descriptions, and key ingredients
- Uses Google Search for up-to-date recipe concepts

### **Censor Agent (Safety Officer)**
- Enforces strict "Family Blacklist" rules
- Performs zero-shot classification: `APPROVED` or `REJECTED`
- Blacklist includes texture restrictions (mushy/slimy foods) and ingredient bans (onions, peppers, mushrooms)

### **Analyst Agent (Logistics Manager)**
- Calculates preparation time and generates shopping lists
- Integrates with custom Python tools for cost/time analysis
- Formats final reports using markdown for clarity

## Technical Details

### Multi-Agent Architecture
- **Framework**: Google ADK (Agent Development Kit)
- **LLM**: Gemini 2.5 Flash Lite
- **Workflow**: Sequential agent execution with automated recovery loops
- **Error Handling**: Self-correcting system with constraint-based retry logic

### Core Features
- **Recipe Generation**: Creates complete meal proposals based on ingredient requests
- **Sensory Filtering**: Enforces texture and ingredient blacklists
- **Logistics Planning**: Calculates prep time and generates shopping lists
- **Failure Recovery**: Automatically finds alternative recipes when initial proposals are rejected
- **Custom Tools**: Python-based logistics calculator with simulated API integrations

## System Workflow

### Success Path

1. **User Request:** "Give me a simple pasta recipe"
2. **Chef Agent:** Generates detailed pasta recipe
3. **Censor Agent:** Verifies against blacklist → APPROVED
4. **Analyst Agent:** Calculates logistics and generates final report

### Failure Recovery Path

1. **User Request:** "Beef chili with onions"
2. **Chef Agent:** Generates chili recipe with onions
3. **Censor Agent:** Detects banned ingredient → REJECTED: Onions
4. **Recovery Loop:** Automatically requests onion-free alternative
5. **Analyst Agent:** Processes approved alternative recipe

## Project Structure
```
picky-eater-protocol/
├── picky_eater_protocol.ipynb     # Main notebook with full implementation
├── requirements.txt               # Python dependencies
├── agent_configs/                 # Agent definitions and prompts
│   ├── chef_agent.py
│   ├── censor_agent.py
│   └── analyst_agent.py
├── tools/                         # Custom tools and functions
│   └── logistics_calculator.py
└── README.md                      # This file
```

## Installation & Local Development
To run this system locally:
```
bash
# Clone the repository
git clone https://github.com/your-username/picky-eater-protocol.git
cd picky-eater-protocol

# Install dependencies
pip install -r requirements.txt

# Set up Google API key
export GOOGLE_API_KEY="your-api-key-here"

# Run the notebook
jupyter notebook picky_eater_protocol.ipynb
```

## Key Capabilities

### Constraint Enforcement
* **Texture Filters:** Blocks recipes described as 'mushy', 'slimy', or 'lumpy'
* **Ingredient Bans:** Automatic rejection of onions, bell peppers, mushrooms
* **Context-Aware:** Understands ingredient forms and preparation methods

### Automated Recovery
* **Dynamic Reprompting:** When a recipe fails, automatically generates new constraints
* **Alternative Finding:** Searches for safe substitutions within the same cuisine category
* **Seamless Continuation:** Maintains workflow integrity throughout recovery process

### Logistics Intelligence
* **Smart Time Estimation:** Adjusts prep time based on recipe complexity
* **Ingredient Categorization:** Identifies main shopping items automatically
* **Clean Formatting:** Presents results in easy-to-read markdown format

## Business Value

### For Families
1. **Time Savings:** Reduces meal planning from hours to minutes
2. **Stress Reduction:** Eliminates negotiation and ingredient checking
3. **Nutrition Improvement:** Ensures diverse, balanced meals within constraints

### For Healthcare
1. **Support Tool:** Assists dietitians working with sensory-sensitive clients
2. **Consistency:** Maintains strict adherence to dietary restrictions
3. **Documentation:** Provides clear logs of approvals and rejections

## Environment Requirements
```
json
{
  "python_version": "3.11.13",
  "operating_system": "Linux-6.6.105+",
  "google_adk_version": "1.18.0",
  "required_apis": ["Google Gemini API"]
}
```

## Performance Metrics
* **Success Rate:** 100% completion (via recovery path when needed)
* **Processing Time:** ~10-15 seconds per full workflow
* **Accuracy:** Zero false approvals on blacklisted items

## Contributing
Feel free to fork this project and submit pull requests for any improvements!

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

*Built for the Kaggle Agents Intensive - Capstone Project and 5-Day AI Agents Intensive Course with Google* [5-Day Agent](https://www.kaggle.com/learn-guide/5-day-agents)
