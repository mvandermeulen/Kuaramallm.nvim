<p align= "center">
<img src="https://github.com/Kurama622/screenshot/raw/master/llm/llm-logo-light-purple-font.png" alt="llm.nvim" width="345">
</p>

---

> [!IMPORTANT]
> This is a universal plugin for a large language model (LLM), designed to enable users to interact with LLM within neovim.
>
> You can customize any LLM (such as gpt, glm, kimi and local LLM) you wish to use.
>
> You can customize some useful tools to complete your tasks more effectively.
>
> Finally, and most importantly, you can use various free models (whether provided by `Cloudflare`, `Github models`, `siliconflow` or others).

<!-- mtoc-start -->

* [Screenshots](#screenshots)
  * [Chat](#chat)
  * [Quick Translate](#quick-translate)
  * [Explain Code](#explain-code)
  * [Customizable LLM application tools](#customizable-llm-application-tools)
    * [Optimize Code](#optimize-code)
    * [Optimize Code and Compare with Original Code in Source File](#optimize-code-and-compare-with-original-code-in-source-file)
    * [Translate](#translate)
* [Installation](#installation)
  * [cloudflare](#cloudflare)
  * [ChatGLM (智谱清言)](#chatglm-智谱清言)
  * [Customized Large Language Model](#customized-large-language-model)
    * [kimi](#kimi)
    * [Github Models](#github-models)
    * [Local LLM](#local-llm)
* [Default Configuration](#default-configuration)
* [Configuration](#configuration)
  * [Example Configuration](#example-configuration)
* [others](#others)
  * [Check Your Account Balance](#check-your-account-balance)
  * [Flexible Window](#flexible-window)

<!-- mtoc-end -->

## Screenshots

https://github.com/user-attachments/assets/1cac9b3c-e03e-478a-9eda-8b1a1856fd89

### Chat

You can converse with it just like you would with ChatGPT.

<p align= "center">
  <img src="https://github.com/Kurama622/screenshot/blob/master/llm/llm-chat-compress.png" alt="llm-chat" width="450">
</p>

### Quick Translate

Select the text to translate quickly. (Support displaying the translation result in a flexible window)

<p align= "center">
  <img src="https://github.com/user-attachments/assets/9b822bce-8384-4d45-9d9a-7007a004084c" alt="llm-translate" width="450">
</p>

### Explain Code

Can't understand the code? Don't worry, AI will explain every code snippet for you. (Support displaying the explanation result in a flexible window)

<p align= "center">
  <img src="https://github.com/Kurama622/screenshot/blob/master/llm/llm-explain-code-compress.png" alt="llm-explain-code" width="450">
</p>

### Customizable LLM application tools

You can customize some useful tools to complete your tasks more effectively. Detailed tutorial can be found on [wiki](https://github.com/Kurama622/llm.nvim/wiki/App-Tools#how-to-add-an-application-tool-to-llmnvim).


#### Optimize Code

Let AI optimize your code. Press `y` to copy the optimized code, and `n` to ignore.

> [!TIP]
> The code implementation can be roughly referred to: [wiki: create-a-tool-to-help-optimize-your-code](https://github.com/Kurama622/llm.nvim/wiki/App-Tools#create-a-tool-to-help-optimize-your-code)
> 
> Currently these functions have been integrated into https://github.com/Kurama622/llm.nvim/blob/main/lua/llm/common/tools.lua and no longer need to be defined.

<p align= "center">
  <img src="https://github.com/Kurama622/screenshot/blob/master/llm/llm-optimize-code-compress.png" alt="llm-optimize-code" width="450">
</p>

```lua
{
  "Kurama622/llm.nvim",
  dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
  cmd = { "LLMSesionToggle", "LLMSelectedTextHandler", "LLMAppHandler" },
  config = function()
    local tools = require("llm.common.tools")
    require("llm").setup({
        app_handler = {
          OptimizeCode = {
            handler = tools.side_by_side_handler,
          }
        }
    })
  end,
  keys = {
    { "<leader>ao", mode = "x", "<cmd>LLMAppHandler OptimizeCode<cr>" },
  },
}
```

#### Optimize Code and Compare with Original Code in Source File

Show the diff between your code and the optimized code in source file. Press `y` to accept the suggestion, and `n` to reject.

> [!TIP]
> The code implementation can be roughly referred to: [wiki: create-a-tool-to-help-optimize-your-code-and-show-the-result-in-source-file](https://github.com/Kurama622/llm.nvim/wiki/App-Tools#create-a-tool-to-help-optimize-your-code-and-show-the-result-in-source-file)
> 
> Currently these functions have been integrated into https://github.com/Kurama622/llm.nvim/blob/main/lua/llm/common/tools.lua and no longer need to be defined.

<p align= "center">
  <img src="https://github.com/Kurama622/screenshot/raw/master/llm/llm-optim-gpt-compress.png" alt="llm-optimize-compare-action" width="450">
</p>

```lua
{
  "Kurama622/llm.nvim",
  dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
  cmd = { "LLMSesionToggle", "LLMSelectedTextHandler", "LLMAppHandler" },
  config = function()
    local tools = require("llm.common.tools")
    require("llm").setup({
        app_handler = {
          OptimCompare = {
            handler = tools.action_handler,
          },
        }
    })
  end,
  keys = {
    { "<leader>ao", mode = "x", "<cmd>LLMAppHandler OptimCompare<cr>" },
  },
}
```

#### Translate

Your next translator is not a translator.

> [!TIP]
> The code implementation can be roughly referred to: [wiki: create-a-translator-tool](https://github.com/Kurama622/llm.nvim/wiki/App-Tools#create-a-translator-tool)
> 
> Currently these functions have been integrated into https://github.com/Kurama622/llm.nvim/blob/main/lua/llm/common/tools.lua and no longer need to be defined.

<p align= "center">
  <img src="https://github.com/user-attachments/assets/ff90b1b4-3c2c-40e6-9321-4bab134710ec" alt="llm-trans" width="450">
</p>

```lua
{
  "Kurama622/llm.nvim",
  dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
  cmd = { "LLMSesionToggle", "LLMSelectedTextHandler", "LLMAppHandler" },
  config = function()
    local tools = require("llm.common.tools")
    require("llm").setup({
        app_handler = {
          Translate = {
            handler = tools.qa_handler,
          },
        }
    })
  end,
  keys = {
    { "<leader>at", mode = "x", "<cmd>LLMAppHandler Translate<cr>" },
  },
}
```
## Installation

### cloudflare

1. You need sign up on [cloudflare](https://dash.cloudflare.com/) and get your account and API key. Then you will find all [models](https://developers.cloudflare.com/workers-ai/models/) on cloudflare, where the models labeled as beta are free.

2. Set `ACCOUNT` and `LLM_KEY` in your zshrc or bashrc
```sh
export ACCOUNT=<Your ACCOUNT>
export LLM_KEY=<Your API_KEY>
```

- lazy.nvim

```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup()
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
      { "<leader>ae", mode = "v", "<cmd>LLMSelectedTextHandler 请解释下面这段代码<cr>" },
      { "<leader>t", mode = "x", "<cmd>LLMSelectedTextHandler 英译汉<cr>" },
    },
  },
```

### ChatGLM (智谱清言)

1. You need sign up on [https://open.bigmodel.cn/](https://open.bigmodel.cn/), and get your account and API key.

2. `LLM_KEY` in your zshrc or bashrc

```bash
export LLM_KEY=<Your API_KEY>
```

- lazy.nvim
```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        max_tokens = 512,
        url = "https://open.bigmodel.cn/api/paas/v4/chat/completions",
        model = "glm-4-flash",
        prefix = {
          user = { text = "😃 ", hl = "Title" },
          assistant = { text = "⚡ ", hl = "Added" },
        },

        save_session = true,
        max_history = 15,

        -- stylua: ignore
        keys = {
          -- The keyboard mapping for the input window.
          ["Input:Submit"]      = { mode = "n", key = "<cr>" },
          ["Input:Cancel"]      = { mode = "n", key = "<C-c>" },
          ["Input:Resend"]      = { mode = "n", key = "<C-r>" },

          -- only works when "save_session = true"
          ["Input:HistoryNext"] = { mode = "n", key = "<C-j>" },
          ["Input:HistoryPrev"] = { mode = "n", key = "<C-k>" },

          -- The keyboard mapping for the output window in "split" style.
          ["Output:Ask"]        = { mode = "n", key = "i" },
          ["Output:Cancel"]     = { mode = "n", key = "<C-c>" },
          ["Output:Resend"]     = { mode = "n", key = "<C-r>" },

          -- The keyboard mapping for the output and input windows in "float" style.
          ["Session:Toggle"]    = { mode = "n", key = "<leader>ac" },
          ["Session:Close"]     = { mode = "n", key = "<esc>" },
        },
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
      { "<leader>ae", mode = "v", "<cmd>LLMSelectedTextHandler 请解释下面这段代码<cr>" },
      { "<leader>t", mode = "x", "<cmd>LLMSelectedTextHandler 英译汉<cr>" },
    },
  },
```

### Customized Large Language Model

1. Add the requested URL.
2. Specify the model you will be using.
3. Set api_type (if your api type is one of "openai", "workers-ai", "zhipu", you can set it) or Customize the streaming processing function (used for parsing the model output).

[wiki: How To Use Custom LLM Models](https://github.com/Kurama622/llm.nvim/wiki/Modify-LLM#how-to-use-custom-llm-models)

#### [kimi](https://github.com/Kurama622/llm.nvim/wiki/Modify-LLM#kimi)

1. Set "api_type" (api_type: "workers-ai", "openai", "zhipu")

- lazy.nvim
```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        max_tokens = 8000,
        url = "https://api.moonshot.cn/v1/chat/completions",
        model = "moonshot-v1-8k", -- "moonshot-v1-8k", "moonshot-v1-32k", "moonshot-v1-128k"
        api_type = "openai",
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
    },
  }
```

2. Use customized "streaming_handler"

- lazy.nvim
```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        max_tokens = 8000,
        url = "https://api.moonshot.cn/v1/chat/completions",
        model = "moonshot-v1-8k", -- "moonshot-v1-8k", "moonshot-v1-32k", "moonshot-v1-128k"

        streaming_handler = function(chunk, line, output, bufnr, winid, F)
          if not chunk then
            return output
          end
          local tail = chunk:sub(-1, -1)
          if tail:sub(1, 1) ~= "}" then
            line = line .. chunk
          else
            line = line .. chunk

            local start_idx = line:find("data: ", 1, true)
            local end_idx = line:find("}]", 1, true)
            local json_str = nil

            while start_idx ~= nil and end_idx ~= nil do
              if start_idx < end_idx then
                json_str = line:sub(7, end_idx + 1) .. "}"
              end
              local data = vim.fn.json_decode(json_str)
              if not data.choices[1].delta.content then
                break
              end

              output = output .. data.choices[1].delta.content
              F.WriteContent(bufnr, winid, data.choices[1].delta.content)

              if end_idx + 2 > #line then
                line = ""
                break
              else
                line = line:sub(end_idx + 2)
              end
              start_idx = line:find("data: ", 1, true)
              end_idx = line:find("}]", 1, true)
            end
          end
          return output
        end
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
    },
  }
```
#### [Github Models](https://github.com/Kurama622/llm.nvim/wiki/Modify-LLM#github-models)

- lazy.nvim
```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        url = "https://models.inference.ai.azure.com/chat/completions",
        model = "gpt-4o",
        max_tokens = 4096,
        api_type = "openai"
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
    },
  }
```

#### Local LLM

Set `LLM_KEY` to `NONE`

- ollama

```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        url = "http://localhost:11434/api/chat", -- your url
        model = "llama3.2:1b",

        streaming_handler = function(chunk, line, assistant_output, bufnr, winid, F)
          if not chunk then
            return assistant_output
          end
          local tail = chunk:sub(-1, -1)
          if tail:sub(1, 1) ~= "}" then
            line = line .. chunk
          else
            line = line .. chunk
            local status, data = pcall(vim.fn.json_decode, line)
            if not status or not data.message.content then
              return assistant_output
            end
            assistant_output = assistant_output .. data.message.content
            F.WriteContent(bufnr, winid, data.message.content)
            line = ""
          end
          return assistant_output
        end,
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
    },
  }
```

## Default Configuration

- floating window

| window       | key          | mode     | desc                                |
| ------------ | ------------ | -------- | -----------------------             |
| Input        | `ctrl+g`     | `i`      | submit your question                |
| Input        | `ctrl+c`     | `i`      | cancel dialog response              |
| Input        | `ctrl+r`     | `i`      | Rerespond to the dialog             |
| Input        | `ctrl+j`     | `i`      | select the next session history     |
| Input        | `ctrl+k`     | `i`      | select the previous session history |
| Output+Input | `<leader>ac` | `n`      | toggle session                      |
| Output+Input | `<esc>`      | `n`      | close session                       |

- split window

| window       | key          | mode     | desc                    |
| ------------ | ------------ | -------- | ----------------------- |
| Input        | `<cr>`       | `n`      | submit your question    |
| Output       | `i`          | `n`      | open the input box      |
| Output       | `ctrl+c`     | `n`      | cancel dialog response  |
| Output       | `ctrl+r`     | `n`      | Rerespond to the dialog |


## Configuration

`llm.nvim` comes with the following defaults, you can override them by passing config as setup param.

https://github.com/Kurama622/llm.nvim/blob/51350dc2028249b2ac04ec3b0763dcaca18bd059/lua/llm/config.lua#L26-L166

### Example Configuration
```lua
  {
    "Kurama622/llm.nvim",
    dependencies = { "nvim-lua/plenary.nvim", "MunifTanjim/nui.nvim" },
    cmd = { "LLMSesionToggle", "LLMSelectedTextHandler" },
    config = function()
      require("llm").setup({
        prompt = "请用中文回答",
        max_tokens = 512,
        model = "@cf/qwen/qwen1.5-14b-chat-awq",
        prefix = {
          user = { text = "😃 ", hl = "Title" },
          assistant = { text = "⚡ ", hl = "Added" },
        },

        save_session = true,              -- if false, history box will not be showed
        max_history = 15,                 -- max number of history
        history_path = "/tmp/history",    -- where to save history

        input_box_opts = {
          relative = "editor",
          position = {
            row = "85%",
            col = 15,
          },
          size = {
            height = "5%",
            width = 120,
          },

          enter = true,
          focusable = true,
          zindex = 50,
          border = {
            style = "rounded",
            text = {
              top = " Enter Your Question ",
              top_align = "center",
            },
          },
          win_options = {
            -- set window transparency
            winblend = 20,
            -- set window highlight
            winhighlight = "Normal:Normal,FloatBorder:FloatBorder",
          },
        },
        output_box_opts = {
          style = "float", -- right | left | above | below | float
          relative = "editor",
          position = {
            row = "35%",
            col = 15,
          },
          size = {
            height = "65%",
            width = 90,
          },
          enter = true,
          focusable = true,
          zindex = 20,
          border = {
            style = "rounded",
            text = {
              top = " Preview ",
              top_align = "center",
            },
          },
          win_options = {
            winblend = 20,
            winhighlight = "Normal:Normal,FloatBorder:FloatBorder",
          },
        },

        history_box_opts = {
          relative = "editor",
          position = {
            row = "35%",
            col = 108,
          },
          size = {
            height = "65%",
            width = 27,
          },
          zindex = 70,
          enter = false,
          focusable = false,
          border = {
            style = "rounded",
            text = {
              top = " History ",
              top_align = "center",
            },
          },
          win_options = {
            winblend = 20,
            winhighlight = "Normal:Normal,FloatBorder:FloatBorder",
          },
        },

        -- LLMSelectedTextHandler windows options
        popwin_opts = {
          relative = "cursor",
          position = {
            row = -7,
            col = 20,
          },
          size = {
            width = "50%",
            height = 15,
          },
          enter = true,
          border = {
            style = "rounded",
            text = {
              top = " Explain ",
            },
          },
        },

        -- stylua: ignore
        keys = {
          -- The keyboard mapping for the input window.
          ["Input:Submit"]  = { mode = "n", key = "<cr>" },
          ["Input:Cancel"]  = { mode = "n", key = "<C-c>" },
          ["Input:Resend"]  = { mode = "n", key = "<C-r>" },

          -- only works when "save_session = true"
          ["Input:HistoryNext"]  = { mode = "n", key = "<C-j>" },
          ["Input:HistoryPrev"]  = { mode = "n", key = "<C-k>" },

          -- The keyboard mapping for the output window in "split" style.
          ["Output:Ask"]  = { mode = "n", key = "i" },
          ["Output:Cancel"]  = { mode = "n", key = "<C-c>" },
          ["Output:Resend"]  = { mode = "n", key = "<C-r>" },

          -- The keyboard mapping for the output and input windows in "float" style.
          ["Session:Toggle"] = { mode = "n", key = "<leader>ac" },
          ["Session:Close"]  = { mode = "n", key = "<esc>" },
        },
      })
    end,
    keys = {
      { "<leader>ac", mode = "n", "<cmd>LLMSessionToggle<cr>" },
      { "<leader>ae", mode = "v", "<cmd>LLMSelectedTextHandler 请解释下面这段代码<cr>" },
      { "<leader>t", mode = "x", "<cmd>LLMSelectedTextHandler 英译汉<cr>" },
    },
  },
```

Finally, here is my personal configuration for reference.

https://github.com/Kurama622/.lazyvim/blob/main/lua/plugins/llm.lua

## others
### Check Your Account Balance

- For siliconflow: https://api.siliconflow.cn/v1/user/info
```lua
  app_handler = {
    -- check siliconflow's balance
    UserInfo = {
      handler = function()
        local key = os.getenv("LLM_KEY")
        local res = tools.curl_request_handler(
          "https://api.siliconflow.cn/v1/user/info",
          { "GET", "-H", string.format("'Authorization: Bearer %s'", key) }
        )
        print("balance: " .. res.data.balance)
      end,
    },
  }
```

### Flexible Window

```lua
  app_handler = {
    WordTranslate = {
      handler = tools.flexi_handler,
      prompt = "Translate the following text to Chinese, please only return the translation",
      opts = {
        fetch_key = function()
          return switch("enable_glm")
        end,
        url = "https://open.bigmodel.cn/api/paas/v4/chat/completions",
        model = "glm-4-flash",
        api_type = "zhipu",
        exit_on_move = true,
        enter_flexible_window = false,
      },
    },
    CodeExplain = {
      handler = tools.flexi_handler,
      prompt = "Explain the following code, please only return the explanation",
      opts = {
        fetch_key = function()
          return switch("enable_glm")
        end,
        url = "https://open.bigmodel.cn/api/paas/v4/chat/completions",
        model = "glm-4-flash",
        api_type = "zhipu",
        enter_flexible_window = true,
      },
    },
  }
```
