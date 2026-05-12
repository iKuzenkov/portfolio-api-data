# Portfolio API Data

## Project Description

This repository provides mock API data for portfolio projects. It is used as a lightweight backend replacement for frontend development and testing `fetch` requests.

The data is structured for multiple applications, including an auto-clicker extension and a product editor system.

This project helps simulate real API responses without requiring a server.

---

## Structure

- `auto-clicker/` — dataset for auto clicker extension
- `product-editor/` — dataset for product editor application

---

## Usage

Instead of using raw `fetch`, you can wrap requests in a reusable utility function.

---

### Generic fetch helper

```ts
async function getFetchData<T>(url: string): Promise<T> {
  const res = await fetch(url);

  if (!res.ok) {
    throw new Error(`HTTP error: ${res.status}`);
  }

  return res.json() as Promise<T>;
}

export default getFetchData;
```

---

### API layer example

```ts
import getFetchData from "../../../api/get-fetch-data-api/getFetchData";
import type { DataInfo } from "./TypesData";

async function infoData(): Promise<DataInfo> {
  return getFetchData<DataInfo>(
    "https://raw.githubusercontent.com/iKuzenkov/portfolio-api-data/main/auto-clicker/how-to-use.json"
  );
}

export default infoData;
```

---

### Example usage in React

```ts
import { useEffect, useState } from "react";
import infoData from "./data/infoData";
import type { DataInfo } from "./data/TypesData";

function Example() {
  const [data, setData] = useState<DataInfo | null>(null);

  useEffect(() => {
    infoData()
      .then(setData)
      .catch(console.error);
  }, []);

  return <div>{data?.title}</div>;
}

export default Example;
```