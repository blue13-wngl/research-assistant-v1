import anthropic 
import datetime
client = anthropic.Anthropic()
search = input(" what would you like to search: ") 
message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=2000,
   messages=[
        {"role": "user", "content": f"find the research then summarize your findings, identify researchers, and suggest futher directions on {search}, format it under 1500 characters."}
    ]
)

print(message.content[0].text)

date = datetime.date.today()
filename = f"/Users/user/cain_root/research_v1/{date}_{search}.md"

with open(filename, "a") as file:
    file.write(message.content[0].text)
print("Research saved.")
