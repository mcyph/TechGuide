# Console Apps: Typer

```bash
python3 -m pip install "typer[all]"
```

```python
import typer

def main(name: str):
    print(f"Hello {name}")

if __name__ == "__main__":
    typer.run(main)
```
