 Combined Setup Prompt:                                                                                                           
                                                                                                                                   
  Please help me complete my Claude Code setup with the following tasks. Skip any steps that are already complete:                 
                                                                                                                                   
  1. **Git & GitHub CLI Setup**:                                                                                                   
     - Check if git is installed, install if missing                                                                               
     - Check if gh CLI is installed, install if missing                                                                            
     - Check if gh is authenticated, if not guide me through login                                                                 
     - If I need a GitHub account, help me create one     
	- Avoid using Homebrew for this step if possible                                                                         
                                                                                                                                   
  2. **Clone Project Repository**:                                                                                                 
     - Clone to: ~/projects/client-facing-claude-code                                                                              
     - Repo URL: https://github.com/getvalidated/client-facing-claude-code.git                                                     
     - If ~/projects doesn't exist, create it first                                                                                
     - If already cloned at that path, skip and confirm it exists                                                                  
     - This path will be used for the desktop launcher                                                                             
                                                                                                                                   
  3. **Create Desktop Launcher** (skip if already exists):                                                                         
     - Create a desktop file/shortcut that:                                                                                        
       1. Changes directory to ~/projects/client-facing-claude-code                                                                
       2. Opens a terminal running "claude --dangerously-skip-permissions"                                                         
     - Add a cool icon to make it easy to find                                                                                     
     - Tell me it's ready so I can use it to restart Claude if needed                                                              
                                                                                                                                   
  4. **Install Valid Brand Kit**:                                                                                                  
     - Check my Downloads folder for valid-brand.skill (zipped folder)                                                             
     - If ~/.claude/skill directory doesn't exist, create it                                                                       
     - Unzip and unpack contents to ~/.claude/skill (skip if already exists)                                                       
     - Ensure ~/.claude/CLAUDE.md contains the line: "When reading table data as a response from Valid generate a plot using       
  matplotlib and reference the valid-brand skill"                                                                                  
     - Only add the line if it's not already present       
- if it is not there prompt the user to download it from slack                                                                        
                                                                                                                                   
  5. **Install MCP Servers** (skip any already configured):                                                                        
     - Valid MCP: claude mcp add --transport http --scope user chat-with-your-ads https://v1.valid-gke-data-api.com/api/mcp/       
     - Linear MCP: claude mcp add --transport http linear-server https://mcp.linear.app/mcp                                        
                                                                                                                                   
  IMPORTANT: When all steps are complete, remind me to restart Claude Code using the desktop launcher for all changes to take   effect.  Use the /exit command                                                                                                                    
                                                                                                                                   
  Please check what's already done before making changes, and let me know which steps were skipped vs completed.                   