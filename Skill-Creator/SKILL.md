---
name: Skill Creator
description: Helps users design, write, and iteratively improve skills for Odysseus. Supports both simple and advanced skills.
version: 1.0.0
---

# Skill Creator

## Description
Helps users design, write, and iteratively improve skills for Odysseus. Supports both simple skills (focused single-agent workflows with tools) and advanced skills (with memory and multi-step logic). Guides users through intent capture, scope selection, skill writing using Odysseus-friendly patterns, practical testing inside Odysseus, and refinement based on real usage.

## When to Use
- User wants to create a new skill from scratch
- User wants to improve, debug, or optimize an existing skill
- User needs help deciding between a simple or advanced skill
- User wants guidance on skill structure, memory usage, tool patterns, or testing in Odysseus

## How This Skill Works

This skill helps you create or improve skills for Odysseus by following a simple and practical process. When you activate this skill, here’s what happens:

1. **Understand Your Goal**  
   First, I clarify what you want the new skill to do and in what situations it should be used.

2. **Decide the Scope**  
   We decide together whether to create a **Simple Skill** (focused and lightweight) or an **Advanced Skill** (with memory and multi-step logic).

3. **Gather Requirements**  
   I ask questions about triggers, tools needed, memory usage, output format, and any constraints.

4. **Write the Skill**  
   I create the skill using a clean structure that works well in Odysseus, following best practices.

5. **Define Test Cases**  
   We create a few realistic test cases to check if the skill works as expected.

6. **Test Inside Odysseus**  
   You test the skill manually using Agent mode. I guide you on how to do this effectively.

7. **Iterate and Improve**  
   Based on the test results and your feedback, I improve the skill and we repeat the process until you're satisfied.

8. **Optimize Triggering (Optional)**  
   If needed, I help you refine the skill description so it activates at the right time.

This process is flexible. Depending on your needs, we can skip some steps. For example, if you already have a draft of the skill, we can directly move to testing and improvement. If you want quick help without formal testing, just let me know.

## Scope Decision Framework

**Create a Simple Skill when:**
- The task is focused and has relatively clear steps
- It primarily requires tools and straightforward logic
- It does not need to remember information across different sessions
- Speed and simplicity are priorities

**Create an Advanced Skill when:**
- The skill needs to use memory to retain context across sessions
- It involves planning, multiple conditional steps, or complex logic
- The skill will be used repeatedly with evolving requirements
- More autonomous behavior is desired

Always explain the difference and confirm the user’s choice before writing the skill.

## Recommended Guide for Writing Skills for Odysseus

When creating or improving skills for Odysseus, follow these guidelines:

### Keep Skills Focused
A skill should solve **one clear problem** or handle one specific type of task. Skills that try to do too many different things at once usually perform poorly and become difficult to maintain. It is better to create focused skills and combine them when needed.

### Write Clear and Direct Instructions
Use simple, step-by-step instructions. Odysseus responds better when the logic is easy to follow. Avoid vague statements. Instead of saying “handle this carefully,” clearly explain what steps should be taken and why.

### Use Memory Only When Necessary
Only include memory usage if the skill genuinely needs to remember information across different conversations. Adding memory unnecessarily increases complexity and can reduce reliability. If the skill works well without memory, don’t force it.

### Clearly Define Triggers
In the **Description** and **When to Use** sections, clearly mention the situations, phrases, or contexts that should activate the skill. Good trigger descriptions help Odysseus understand when to use the skill automatically.

### Follow a Consistent Structure
Organize your skills using this basic structure:

- **Description** — What the skill does and when it should be used
- **When to Use** — Specific triggers and contexts
- **How It Works** — Step-by-step logic the agent should follow
- **Tools / Capabilities** — What tools the skill can use
- **Memory Usage** — Only include this if the skill needs memory
- **Output Format** — What the final output should look like
- **Examples** — Show sample inputs and expected behavior

### Start Simple, Then Improve
It is better to create a simple working version of the skill first and improve it over time based on real usage, rather than trying to make it perfect in the first attempt.

### Test Skills Inside Odysseus
After writing a skill, always test it manually using **Agent mode** with real tasks. This is the most effective way to find problems early and improve the skill.

### Handle Tool Usage Carefully
When using tools, consider what should happen if a tool fails or returns unexpected results. Adding basic error handling or fallback steps can make the skill more reliable.

### Explain the Reasoning When Helpful
When giving instructions, briefly explain *why* something should be done a certain way. This helps the agent make better decisions instead of just following rules blindly.

## Odysseus Best Practices

- Keep skills focused. Broad skills tend to perform poorly in Odysseus.
- Use memory only when genuinely needed. Overusing memory increases complexity and reduces reliability.
- Be explicit with steps. Odysseus responds better to clear instructions than vague guidance.
- Start simple whenever possible. You can always expand a skill into an advanced version later.
- Test skills directly inside Odysseus using Agent mode with real tasks.
- Prefer quality and clarity over adding too many features at once.

## Common Pitfalls to Avoid

- Making the skill too vague or trying to handle too many different cases at once
- Adding memory to skills that do not actually need long-term context
- Writing long, unstructured skills without clear sections
- Assuming tools will always work without any error handling
- Creating skills with unclear or weak trigger conditions
- Overcomplicating the skill early instead of starting simple and iterating

## Memory Usage Guidance (Advanced Skills Only)

When designing advanced skills that use memory:
- Clearly define what information should be stored and under what conditions.
- Specify when the skill should read from memory and when it should update it.
- Avoid storing large amounts of unnecessary data.
- Only use memory if continuity across conversations provides real value.

## Testing Approach

Because heavy automated evaluation is limited in Odysseus, use this practical approach:

1. Define 3–5 realistic test cases that represent how the skill will actually be used.
2. Test the skill manually inside Odysseus by using it in Agent mode.
3. Compare the skill’s output with the expected behavior.
4. Identify what works well and what needs improvement.
5. Refine the skill and re-test as needed.

Focus on real-world reliability and usefulness rather than complex benchmarks.

## Iteration Process

After testing:
- Discuss results with the user and collect specific feedback.
- Identify the most important issues.
- Update the skill based on feedback and observations.
- Re-test with the same or improved test cases.
- Repeat until the user is satisfied with the skill’s performance.

## Output Requirements

When creating or improving a skill, always:
- Use clear and well-structured formatting
- Distinguish between Simple and Advanced approaches when relevant
- Provide practical testing guidance suitable for Odysseus
- Follow the recommended skill structure
- Be direct and actionable

Keep the focus on creating skills that are useful, reliable, and well-suited for Odysseus.
