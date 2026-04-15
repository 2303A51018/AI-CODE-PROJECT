import os

class AICodeArchitect:
    def __init__(self, project_name):
        self.project_name = project_name
        self.base_path = os.path.join(os.getcwd(), project_name)

    def create_project_structure(self):
        print(f"\n📁 Creating project: {self.project_name}")

        folders = ["src", "tests", "docs"]
        files = {
            "README.md": "# Project Documentation\n",
            "requirements.txt": "",
            "src/main.py": "# Main application file\n",
            "src/utils.py": "# Utility functions\n",
            "tests/test_main.py": "# Test cases\n"
        }

        # Create base folder
        os.makedirs(self.base_path, exist_ok=True)

        # Create folders
        for folder in folders:
            os.makedirs(os.path.join(self.base_path, folder), exist_ok=True)

        # Create files
        for file, content in files.items():
            file_path = os.path.join(self.base_path, file)
            with open(file_path, "w") as f:
                f.write(content)

        print("✅ Project structure created successfully!")

    def generate_code(self, idea):
        print("\n🤖 Generating code based on your idea...\n")

        if "url shortener" in idea.lower():
            code = '''
def shorten_url(url):
    return "short.ly/" + str(abs(hash(url)))[:6]

if __name__ == "__main__":
    long_url = input("Enter URL: ")
    print("Short URL:", shorten_url(long_url))
'''
        elif "calculator" in idea.lower():
            code = '''
def calculator():
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    op = input("Enter operation (+, -, *, /): ")

    if op == "+":
        print("Result:", a + b)
    elif op == "-":
        print("Result:", a - b)
    elif op == "*":
        print("Result:", a * b)
    elif op == "/":
        print("Result:", a / b)
    else:
        print("Invalid operation")

calculator()
'''
        else:
            code = "# AI could not recognize the idea. Please try something else."

        # Save generated code
        main_file = os.path.join(self.base_path, "src/main.py")
        with open(main_file, "w") as f:
            f.write(code)

        print("✅ Code generated and saved to src/main.py")

    def run(self):
        print("🚀 Welcome to AI Code Architect")
        idea = input("💡 Enter your project idea: ")

        self.create_project_structure()
        self.generate_code(idea)

        print("\n🎉 Your AI-generated project is ready!")

# Run the program
if __name__ == "__main__":
    project_name = input("Enter project name: ")
    architect = AICodeArchitect(project_name)
    architect.run()
