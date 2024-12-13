## Setting Up a Modern React Project with Vite, TailwindCSS, ShadCN, and Vite


### Prerequisites

Before starting, make sure you have the following installed:
- Node.js (v14 or later)
- npm or yarn


#### 1. Create a New Vite React Project

To get started, we first create a new Vite-based React project using the following command:

```
npm create vite@latest my-project -- --template react
```
Or, if you prefer yarn:
```
yarn create vite@latest my-project --template react
```

#### 2. Navigate to the Project Directory

Once your project is created, navigate into the project folder:

```
cd my-project
```
#### 3. Install Dependencies

Install the project dependencies with npm:

```
npm install
```

#### 4. Configure Vite for Custom Port

Open the `vite.config.js` file and configure the server to run on port 3030:

```
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3030
  }
})
```

#### 5. Upgrade Your React Project to v19 (or Latest)

Upgrade React and ReactDOM to version 19 or the latest version by running the following command:

```
npm install react@latest react-dom@latest
```

This ensures that you're using the latest features and improvements in React, providing you with a better development experience.

#### 6. Install TailwindCSS, PostCSS, and Autoprefixer

Add TailwindCSS, PostCSS, and Autoprefixer for styling:

```
npm install -D tailwindcss postcss autoprefixer
```

#### 7. Initialize TailwindCSS

Run the following command to initialize TailwindCSS configuration:
```
npx tailwindcss init -p
```

This will generate two configuration files: `tailwind.config.js` and `postcss.config.js`.

#### 8. Configure TailwindCSS

In `tailwind.config.js`, configure the content paths to ensure TailwindCSS works with your project files:

```
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
};
```
#### 9. Create Global CSS File for Tailwind

In `src/index.css`, add the following imports for TailwindCSS to work:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### 10. Add TailwindCSS Styling to Your App

In `src/App.jsx`, replace the default content with TailwindCSS classes:

```
export default function App() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  );
}
```

#### 11. Run the Development Server

Finally, run the development server:

```
npm run dev
```
#

### Defining Aliases for Easier Imports

Before integrating ShadCN components, let’s define an alias to simplify imports from the `src` folder.

#### 1. Define Alias in Vite Configuration

In `vite.config.js`, import `path` and define an alias for the `src` folder:

```
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from "path";

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3030
  },
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})

```
#### 2. Configure `jsconfig.json` for Aliases

To ensure the alias works in your editor, create or update the `jsconfig.json` file with the following content:

```
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
  }
}
```

#

### Integrating ShadCN for UI Components

Now, let’s integrate ShadCN to enhance the UI with pre-built, customizable components.

#### 1. Initialize ShadCN

Run the following command to initialize ShadCN and customize the UI components:

```
npx shadcn@latest init
```
When prompted, choose the following:
- **Style** : New York
- **Base color** : Zinc
- **Use CSS variables for theming** : Yes

#### 2. Update TailwindCSS Config for ShadCN

In `tailwind.config.js`, import `tailwindcss-animate` and configure the content paths for ShadCN components:

```
import tailwindcssAnimate from 'tailwindcss-animate';

module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,jsx,ts,tsx}",
    "./node_modules/@shadcn/**/*.{js,jsx,ts,tsx}",
  ],
  plugins: [tailwindcssAnimate],
};
```

#### 3. Install `tailwindcss-animate` Plugin

To enable animations in ShadCN components, install `tailwindcss-animate`:

```
npm install tailwindcss-animate
```

#### 4.  Add ShadCN Components

After initializing ShadCN, you can add UI components such as Buttons, Cards, Input, Label, Select etc. For example, to add the Button component, run:
```
npx shadcn@latest add button card input label select
```

This will automatically install the necessary dependencies for the components and add them to your project.

#### 5. Use ShadCN Components in Your App

Now, you can use the ShadCN components in your `App.jsx` or any other component. For example:

```
import * as React from "react"
 
import { Button } from "@/components/ui/button"
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select"

export default function App() {
  return (
    <div className="flex justify-center items-center min-h-screen bg-black">
    <Card className="w-[350px]">
      <CardHeader>
        <CardTitle>Create project</CardTitle>
        <CardDescription>Deploy your new project in one-click.</CardDescription>
      </CardHeader>
      <CardContent>
        <form>
          <div className="grid w-full items-center gap-4">
            <div className="flex flex-col space-y-1.5">
              <Label htmlFor="name">Name</Label>
              <Input id="name" placeholder="Name of your project" />
            </div>
            <div className="flex flex-col space-y-1.5">
              <Label htmlFor="framework">Framework</Label>
              <Select>
                <SelectTrigger id="framework">
                  <SelectValue placeholder="Select" />
                </SelectTrigger>
                <SelectContent position="popper">
                  <SelectItem value="react">React.js</SelectItem>
                  <SelectItem value="next">Next.js</SelectItem>
                  <SelectItem value="sveltekit">SvelteKit</SelectItem>
                  <SelectItem value="astro">Astro</SelectItem>
                  <SelectItem value="nuxt">Nuxt.js</SelectItem>
                </SelectContent>
              </Select>
            </div>
          </div>
        </form>
      </CardContent>
      <CardFooter className="flex justify-between">
        <Button variant="outline">Cancel</Button>
        <Button>Deploy</Button>
      </CardFooter>
    </Card>
    </div>
  );
}

```




#### 6. Run the Development Server Again

After completing the configuration, run the development server again:

```
npm run dev
```

# 

### Conclusion

By following this guide, you have successfully set up a React project with Vite, integrated TailwindCSS for styling, and added ShadCN components for a more efficient and visually appealing user interface. Whether you are using npm or yarn, the process remains the same, offering flexibility based on your package manager preference.

### Key Takeaways

- Vite is a fast and modern tool for React projects.
- TailwindCSS provides utility-first styling, making it easier to design and maintain your frontend.
- ShadCN components speed up UI development with pre-built, customizable elements.
- With `tailwindcss-animate`, you can add animations to ShadCN components effortlessly.



## License

This guide is licensed under the [MIT License](./LICENSE).
