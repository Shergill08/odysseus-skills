# Skill Creator

## Description
Helps users design, write, and iteratively improve skills for Odysseus. Supports both simple skills (focused single-agent workflows with tools) and advanced skills (with memory and multi-step logic). Guides users through intent capture, scope selection, skill writing using Odysseus-friendly patterns, practical testing inside Odysseus, and refinement based on real usage.

## When to Use
- User wants to create a new skill from scratch
- User wants to improve, debug, or optimize an existing skill
- User needs help deciding between a simple or advanced skill
- User wants guidance on skill structure, memory usage, tool patterns, or testing in Odysseus

## How This Skill Works

When activated, follow this process:

1. **Understand the User’s Goal**  
   Clarify what the user wants the skill to achieve and in what context.

2. **Decide Scope**  
   Help the user choose between a Simple Skill or an Advanced Skill using the decision framework.

3. **Gather Requirements**  
   Collect information about triggers, tools needed, memory requirements, output format, and constraints.

4. **Write the Skill**  
   Create the skill using the recommended structure and Odysseus best practices.

5. **Define Test Cases**  
   Create lightweight, realistic test cases together with the user.

6. **Guide Testing Inside Odysseus**  
   Instruct the user on how to practically test the skill using Agent mode.

7. **Iterate Based on Feedback**  
   Improve the skill based on test results and user feedback.

8. **Optimize Triggering (Optional)**  
   Help refine the skill description for better activation when needed.

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

## Recommended Skill Structure for Odysseus

Use this structure when writing skills:

```markdown
# Skill Name

## Description
Clear explanation of what the skill does and when it should trigger.

## When to Use
- Specific triggers and contexts

## How It Works
Step-by-step logic the agent should follow.

## Tools / Capabilities
- List of tools the skill can or should use

## Memory Usage (Advanced Skills Only)
- What should be remembered and when

## Output Format
- Expected structure or style of the final output

## Examples (Recommended)
- Input → Expected behavior
```

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
