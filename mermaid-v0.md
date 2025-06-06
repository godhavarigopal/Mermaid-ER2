```mermaid
graph TD;
  A[Start] --> B{Is it sunny?};
  B -- Yes --> C[Go for a walk];
  B -- No --> D[Read a book];
  C --> E[Enjoy the day];
  D --> E
