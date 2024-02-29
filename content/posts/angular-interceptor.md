---
author: ["nove-b"]
title: "AngularでAPIリクエスト前後の処理を共通化する"
date: "2024-02-29 10:38:05"
description: "AngularでAPIコール前にAuthorizationを持たせる必要があったのでHttpInterceptorを使用してみた"
tags: ["Angular"]
ShowToc: true
draft: false
---

## 環境
```bash
node => v16.13.2
angular => 15.0.4
```

## AngularでリクエストヘッダーにAuthorizationを共通して持たせたい

とかレスポンスの`StatusCode`を見て共通処理を書くと言ったAPIリクエスト前後の処理をどこで実装するのがいいのか調べてみた。

## HttpInterceptor

どうやらドンピシャっぽいのがこれで、[ドキュメント](https://angular.jp/api/common/http/HttpInterceptor#description)によると

> Intercepts and handles an HttpRequest or HttpResponse.

つまり、リクエストとレスポンスそれぞれに処理をできますよということ。まさに探していた機能に間違いない。

## 使ってみる

### リクエストに対して処理をする

``` typescript
import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
} from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor() {}
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    const newReq = req.clone({
      headers: req.headers.set(
        'Authorization',
        'Bearer ' + 'token'
      ),
    });
    // cloneされてヘッダーを付与したリクエストを次の処理に引き渡す
    return next.handle(newReq);
  }
}
```
これでリクエストヘッダーに`Bearer token`という`Authorization`が付与されたうえでリクエストが投げられる。

### レスポンスに対して処理をする

```typescript
import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
} from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable, catchError } from 'rxjs';
import { MatDialog } from '@angular/material/dialog';

@Injectable()
export class ErrorInterceptor implements HttpInterceptor {
  constructor(public dialog: MatDialog) {}
  intercept(
    request: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    const req = request.clone();
    return next.handle(req).pipe(
      catchError((res) => {
        if (400 <= res.status && res.status < 500 ) {
          console.log('400以上500未満のエラーが発生しました。')
        }

        return next.handle(req).pipe();
      })
    );
  }
}
```
これでレスポンスの`status`が400以上500未満の場合に限り`console`が発火するようになった。
これを使用すれば各`status`に対する共通の処理を書くことができる。

## app.module.ts にプロバイダー登録

それぞれ処理を書いたら`app.module.ts`の`providers`に登録する。

```typescript
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true },
    { provide: HTTP_INTERCEPTORS, useClass: ErrorInterceptor, multi: true },
  ],
```

これで無事に求めている動きをするようになった。


