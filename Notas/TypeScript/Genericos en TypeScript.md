
```ts

type Books = {
    author: string;
    title: string;
    price: number;
}

type ActionsTypes = `update-${keyof Books}`;

type Actions<T, K extends keyof T & string> = {
    type: `update-${K}`,
    payload: T[K]
}

type UpdateTitleAction = Actions<Books, 'title'>;

type Linked<T> = {
    value: T,
    next?: Linked<T>
}

const TextLinked: Linked<string> = {
    value: "Hello",
    next: {
        value: "World"
    }
}

const buildLink = <T,>(value: T, next?: Linked<T>): Linked<T> => {
    return {
        value,
        next
    }
}

const stringLink = buildLink('high');


export const ceateContext = <T extends {}>() => {
    const Context = React.createContext<T | undefined>(undefined);

    const useContext = () => {
        const colorContext = React.useContext(Context);

        if(ceateContext === undefined){
            throw new Error('A value must be provided to the useContext.')
        }

        return colorContext;
    }

    return [useContext, Context.Provider] as const;
}
```
