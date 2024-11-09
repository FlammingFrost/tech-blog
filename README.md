# Costomize the Blog
## Configration
To edit the configration of this theme, you need to go to `/config` and edited the `.toml` file here. Generally, the configration file will be overwritten in following sequence:

`/config/path/config.toml`>`config.toml`>`theme/your-theme/config.toml`

For hugo version $\geq$`0.115`, the `config.toml` will be replaced by `hugo.toml`. Similary, `config.toml` has the same function and `config.yaml`, except for the grammar.

## Edit column on upper right
There are **2** places should be edited:
### 1. In `/config/_default/menus.toml`
```toml
[[main]]
    # Top-level menu entry
    identifier = "work"
    name = "Work"
    url = "/projects/"
    weight = 1

[[main]]
    identifier = "projects"
    name = "Projects"
    url = "/projects/"
    parent = "work"
    weight = 2

[[main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    parent = "work"
    weight = 1

[[main]]
    identifier = "contact"
    name = "Contact"
    url = "/contact/"
    parent = "work"
    weight = 3
```
In example show above, Work is the parent botton, and "project", "about" and "contact" are three children. They will show as a list when the mouse float on the "work" button.
Here are some params.:
- `identifier`: specify the parent and childern.
- `name`: The text on the button.
- `url`: your post folder address, pay attention to you folder structure.
- `parent`: as it goes. For example, when the mouse float on the "Writing" button, its children will show.
- `weight`: Decide the rank children shown. The smallest one will be on the top.

### 2. folder structure
1. create a folder of your new column in `/content/`, for example, `/content/new_column/`.
2. create a `_index.md` in `/content/new_column/`.