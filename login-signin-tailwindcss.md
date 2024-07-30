## こんなデザインができます
色々なwebアプリのデザインに使える新規登録とログイン画面です。

![スクリーンショット 2024-07-17 224125.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/986141/dbe12ffa-3f05-de59-a910-591fc38ce7a4.png)

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/986141/43f318f0-a9c5-d3e5-075d-c701fbf5ffec.png)


## 新規登録

```tsx
'use client';
import React from "react";
import { useForm } from "react-hook-form";
import Link from "next/link";

type Inputs = {
    email: string;
    password: string;
};

const Register = () => {
    const { register, handleSubmit, formState: { errors } } = useForm<Inputs>();

    return (
        <div className="flex flex-col items-center justify-center h-screen">
            <form className="w-96 p-8 bg-white rounded-lg shadow-md">
                <h1 className="mb-4 text-2xl font-medium text-grey-700">新規登録</h1>
                <div className="mb-4">
                    <label className="block text-sm font-medium text-grey-600">メールアドレス</label>
                    <input
                        {...register("email", {
                            required: "メールアドレスは必須です",
                            pattern: {
                                value: /^[a-zA-Z0-9_.+-]+@([a-zA-Z0-9][a-zA-Z0-9-]*[a-zA-Z0-9]*\.)+[a-zA-Z]{2,}$/,
                                message: "このメールアドレスは無効です。",
                            },
                        })}
                        type="email"
                        placeholder="mail@myservice.com"
                        className="w-full p-2 mt-1 border-2 rounded-md"
                    />
                    {errors.email && (
                        <span className="text-sm text-red-600">{errors.email.message}</span>
                    )}
                </div>
                <div className="mb-4">
                    <label className="block text-sm font-medium text-grey-600">パスワード</label>
                    <input
                        {...register("password", {
                            required: "パスワードは必須です",
                            minLength: {
                                value: 8,
                                message: "パスワードは8文字以上でなくてはなりません",
                            },
                        })}
                        type="password"
                        className="w-full p-2 mt-1 border-2 rounded-md"
                    />
                    {errors.password && (
                        <span className="text-sm text-red-600">{errors.password.message}</span>
                    )}
                </div>
                <div className="flex justify-end">
                    <button type="submit" className="px-4 py-2 font-bold text-white bg-blue-500 rounded hover:bg-blue-700">
                        新規登録
                    </button>
                </div>
                <div className="mt-4">
                    <span className="text-sm text-grey-600">既にアカウントをお持ちですか？</span>
                    <Link href="/path/login" className="ml-1 text-sm font-bold text-blue-500 hover:text-blue-700">
                        ログインページはこちら
                    </Link>
                </div>
            </form>
        </div>
    );
};

export default Register;
```

## ログイン
```tsx
'use client';
import React from "react";
import { useForm } from "react-hook-form";
import Link from "next/link";

type Inputs = {
    email: string;
    password: string;
};

const Login = () => {
    const { register, handleSubmit, formState: { errors } } = useForm<Inputs>();
    return (
        <div className="flex flex-col items-center justify-center h-screen">
            <form className="w-96 p-8 bg-white rounded-lg shadow-md">
                <h1 className="mb-4 text-2xl font-medium text-grey-700">ログイン</h1>
                <div className="mb-4">
                    <label className="block text-sm font-medium text-grey-600">メールアドレス</label>
                    <input
                        {...register("email", {
                            required: "メールアドレスは必須です",
                            pattern: {
                                value: /^[a-zA-Z0-9_.+-]+@([a-zA-Z0-9][a-zA-Z0-9-]*[a-zA-Z0-9]*\.)+[a-zA-Z]{2,}$/,
                                message: "このメールアドレスは無効です。",
                            },
                        })}
                        type="email"
                        placeholder="mail@myservice.com"
                        className="w-full p-2 mt-1 border-2 rounded-md"
                    />
                    {errors.email && (
                        <span className="text-sm text-red-600">{errors.email.message}</span>
                    )}
                </div>
                <div className="mb-4">
                    <label className="block text-sm font-medium text-grey-600">パスワード</label>
                    <input
                        {...register("password", {
                            required: "パスワードは必須です",
                            minLength: {
                                value: 8,
                                message: "パスワードは8文字以上でなくてはなりません",
                            },
                        })}
                        type="password"
                        className="w-full p-2 mt-1 border-2 rounded-md"
                    />
                    {errors.password && (
                        <span className="text-sm text-red-600">{errors.password.message}</span>
                    )}
                </div>
                <div className="flex justify-end">
                    <button type="submit" className="px-4 py-2 font-bold text-white bg-blue-500 rounded hover:bg-blue-700">
                        ログイン
                    </button>
                </div>
                <div className="mt-4">
                    <span className="text-sm text-grey-600">初めてのご利用の方は</span>
                    <Link href="/path/register" className="ml-1 text-sm font-bold text-blue-500 hover:text-blue-700">
                        こちら
                    </Link>
                </div>
            </form>
        </div>
    );
};

export default Login;
```

## 挙動について
formタグの`onSubmit`属性を定義していないので、新規登録とログインボタンを押した後の挙動は省略されています。
ただそれだけでは味気ないので、`react-hook-form`からインポートした`useForm`メソッドを使ってメールアドレスやパスワードの入力値に条件を付ける処理を入れました。

https://react-hook-form.com/docs/useform/register

例えば、「＠」がないとこのようなアラートが出ます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/986141/2397b99a-5206-1d7e-47c2-ece80671cac1.png)
