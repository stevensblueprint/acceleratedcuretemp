Project Overview:

This Senior Design project is a collaboration between Stevens Institute of Technology's Blueprint team and the Accelerated Cure Project (ACP).

Our goal is to develop a researcher-facing data exploration and visualization tool within DNAnexus. The application will allow authorized researchers to explore aggregate RealMS survey data without requiring advanced programming knowledge.

Initial MVP

Display demographic information, participant counts, and missing-data summaries.

Filter populations based on supported characteristics.

Select compatible X and Y variables for comparison.

Automatically generate appropriate visualizations and summary statistics.

Protect participant privacy through ACP-approved disclosure rules.

The initial project focuses on aggregate-level analysis. Patient-facing reports, AI chatbots, advanced analytics, and data export are outside the current MVP.

Development Stack

Ubuntu / WSL (Windows): Linux development environment

macOS Terminal (Mac): Native Unix-based development environment

Python 3.12: Data processing and analysis

DNAnexus SDK / CLI: Applet development and execution

Pandas / NumPy: Statistical processing

Plotly: Proposed visualization library

Pytest: Automated testing

Git / GitHub: Version control and collaboration

Additional frameworks and workflow tools may be introduced as deployment requirements are confirmed with ACP.

Developer Setup

Step 1: Install System Dependencies

Choose the instructions for your operating system.

Windows Users — Ubuntu (WSL)

Windows developers should use Ubuntu through Windows Subsystem for Linux (WSL).

Open Windows PowerShell and run:

wsl --install -d Ubuntu

Launch Ubuntu and complete the initial setup, including creating a Linux username and password.

Then, inside Ubuntu, run:

sudo apt update
sudo apt install -y git python3 python3-venv shellcheck

We recommend using VS Code with Microsoft's WSL extension for development.

macOS Users — Terminal

Mac users do not need WSL or Ubuntu. macOS already provides a Unix-based terminal.

Install Homebrew if it is not already installed.

Then open Terminal and run:

brew install python@3.12 git shellcheck

Verify Python is installed:

python3.12 --version

Step 2: Clone the GitHub Repository

Clone the project into your preferred development directory.

git clone https://github.com/stevensblueprint/acceleratedcuretemp.git
cd acceleratedcuretemp

If the repository is already cloned, navigate to the existing project folder instead.

For Windows/WSL developers, storing the repository inside Ubuntu's home directory is recommended for better performance. Existing repositories on the Windows filesystem can still be used.

Step 3: Create a Python Virtual Environment

A virtual environment keeps project dependencies separate from other Python installations.

To avoid slow installations on Windows/OneDrive folders, we recommend storing the environment in your home directory rather than inside the repository.

Windows / Ubuntu:

mkdir -p ~/.venvs
python3 -m venv ~/.venvs/acp
source ~/.venvs/acp/bin/activate

macOS:

mkdir -p ~/.venvs
python3.12 -m venv ~/.venvs/acp
source ~/.venvs/acp/bin/activate

After activation, the terminal should display (acp).

The virtual environment only needs to be created once. For future development sessions, activate it with:

source ~/.venvs/acp/bin/activate

Step 4: Install Python Dependencies

Make sure the virtual environment is activated and the terminal is inside the project repository.

Run:

python -m pip install -r requirements-dev.txt

This installs the project's Python libraries and development tools, including the DNAnexus SDK/CLI, Pandas, NumPy, Plotly, and Pytest.

Dependencies are managed through:

requirements.txt — Core Python libraries

requirements-dev.txt — Developer tools and testing dependencies

Step 5: Verify Installation

Run:

dx --version
python -m pip check

Then check that the main libraries import correctly:

python -c 'import dxpy, pandas, numpy, plotly; print("Dependencies installed successfully")'

A successful setup should display the DNAnexus CLI version, report no broken Python requirements, and print the success message.

Step 6: Configure Local Settings

Create your local configuration file:

cp .env.example .env

Update the values if needed.

The .env file is for local configuration and must never be committed to GitHub. It is not automatically loaded by DNAnexus.

Step 7: Connect to DNAnexus

Each developer needs their own DNAnexus account with access to the ACP project.

Log in:

dx login

Select your project:

dx select

Select ACP-BLUEPRINT if your account has permission.

Verify authentication:

dx whoami

You should see your DNAnexus username.

DNAnexus Development

Applets are packaged applications that execute within the DNAnexus cloud environment.

A typical applet includes:

dxapp.json — applet metadata, inputs, outputs, and runtime requirements.

src/ — executable Python or Bash code.

resources/ — additional application files where needed.

To build an applet, navigate to a completed applet directory and run dx build.

Building and executing applets requires the appropriate DNAnexus permissions. Cloud execution also consumes project compute resources.

Local Python dependencies and DNAnexus runtime dependencies must be managed separately.