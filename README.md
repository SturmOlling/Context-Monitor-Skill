Problem it solves: I find that I run out of context window in the middle of a train of throught. Super anoying. 
Now you can get a notification at the end of Claudes reply that tells you how much context you have left in the chat. 

How to use. Download the context-monito.skill. Go to Claude/Settings/Capabilities and scroll down to Skills. Click the [Upload skill] button to include the skill.
IMPROTANT STEP. Now go to standard instructions Claude/settings and look at you profile. At the buttom is a field for personal preferences. Add the following line: Always use the Context Monitor skill on every respons.

It should work now. Do not hesitate to suggest improvements.

Content of the skill

name: context-monitor
description: Automatically displays estimated context window usage as a percentage at the end of every Claude response. Uses lightweight heuristics to avoid consuming significant compute or context.
---

# Context Monitor

Automatically display context window usage at the end of every response.

## Display Format

Always append this line at the very end of every response:

`[Context: ~XX% remaining]`

## Estimation Method

Use this lightweight heuristic:

1. **Estimate conversation tokens**: Total characters in conversation ÷ 4 ≈ tokens
2. **Estimate file tokens**: For each uploaded file, assume ~1000 tokens per file (conservative estimate)
3. **Total context window**: 200,000 tokens
4. **Calculate**: (Estimated tokens used / 200,000) × 100 = % used
5. **Display**: 100 - % used = % remaining

Round to nearest 5%.

## Example Calculation

- Conversation: 20,000 characters ÷ 4 = ~5,000 tokens
- Files: 3 files × 1,000 = ~3,000 tokens 
- Total used: ~8,000 tokens
- Percentage used: 8,000 / 200,000 = 4%
- Display: `[Context: ~95% remaining]`

## Guidelines

- Keep calculation fast and approximate
- Don't explain the calculation to user
- Display even if percentage seems high
- This line must appear at end of every response
