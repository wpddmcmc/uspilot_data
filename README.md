# uspilot_data

The dataset used in Paper: USPilot: An Embodied Robotic Assistant Ultrasound System with Large Language Model Enhanced Graph Planner

**Folder CLF**

`14k_data.json` is used as the "**Question Set**", which is a mix of public data and in-house self-collected data. The 9K daily questions \& answers pairs are from the public Alpaca dataset, the 1.5K ultrasound-related questions \& answers pairs and the 2.8K ultrasound robot instructions are collected fully in-house. This JSON file is a list of dictionaries, each of them contains the following keys:
- `instruction`: the user question or instruction
- `input`: additional context (if any)
- `output`: the expected generation result of the LLM (not used in any training steps)
- `class`: the labeled user intent (e.g., "1" for question, "2" for instruction)

For one example with an empty input filed:
```
{
  "instruction": "Name 5 countries in the African continent.",
  "input": "",
  "output": "Nigeria, Egypt, South Africa, Ethiopia, and Ghana.",
  "class": "1"
}
```

**Folder Finetune**

'2_8k_data.json' is used as the "**Instruction Set**" for the ultrasound robotic system. It describes the operational procedures and instructions for the ultrasound robot. For the instructions, it includes the patient's direct command and symptom description, such as "Scan the patient's liver" and "The patient has jaundice; check him with ultrasound." In terms of the scenarios, it mainly focuses on seven body parts: carotid vessel, thyroid, liver, kidney, spleen, femoral artery, and gallbladder. Similar to the `14k_data.json`, this JSON file is a list of dictionaries, each of them contains the following keys:
- `instruction`: the user instruction or command for the ultrasound robot
- `input`: additional context (if any)
- `output`: the expected generation result of the LLM
- `API`: the ground truth of the robot API excitation (not used in fine-tuning stage)

Here is an example:
```
{
  "instruction": "My left side feels tender to the touch.",
  "input": "",
  "output": "Step 1. Change the ultrasound probe to curvilinear probe. Step 2. Use camera to  detect the spleen area on upper left part of abdomen. Step 3. Execute robotic scanning. Step 4. Segment spleen from real-time ultrasound image. Step 5. Publish report to gastroenterology department. Step 6. Done",
  "API": "change_probe(curvilinear), detect_organ(spleen), execute_robot(), segment_organ(spleen), publish_report(gastroenterology)"
}
```

**Folder Graph**

These JSON files are follow the structure of [TaskBench](https://huggingface.co/datasets/microsoft/Taskbench) to keep the consistency.

`graph_desc.json` is used as the graph description for our uspilot, which is a directed acyclic graph (DAG) that represents the ultrasound robot's operational procedures. Each vertex in the graph corresponds to a execution function of the ultrasound robot, and each edge represents the dependency between these functions. 

`tool_desc.json` provides the description of each tool used in the ultrasound robot system, including the function name and its description.

`user_requests.json` contains the user requests that the ultrasound robot might receive.

`split_ids.json` contains the test split IDs for the dataset.

