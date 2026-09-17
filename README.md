# CORS (NestJS)

**Source:** https://docs.nestjs.com/security/cors

Cross-origin resource sharing (CORS) হলো একটা mechanism, যেটা অন্য একটা domain থেকে resource request করার সুযোগ দেয়। এর ভেতরে, Nest underlying platform অনুযায়ী Express এর [cors](https://github.com/expressjs/cors) অথবা Fastify এর [@fastify/cors](https://github.com/fastify/fastify-cors) package ব্যবহার করে। এই package গুলো বিভিন্ন option দেয়, যেগুলো তোমার প্রয়োজন অনুযায়ী customize করা যায়।

---

## 1. শুরু করা

CORS enable করার জন্য, Nest application object এ `enableCors()` method call করো।

```typescript
const app = await NestFactory.create(AppModule);
app.enableCors();
await app.listen(process.env.PORT ?? 3000);
```

`enableCors()` method একটা optional configuration object argument নেয়। এই object এর available property গুলো official [CORS](https://github.com/expressjs/cors#configuration-options) documentation এ describe করা আছে। আরেকটা উপায় হলো, একটা [callback function](https://github.com/expressjs/cors#configuring-cors-asynchronously) পাস করা, যেটা দিয়ে request অনুযায়ী (on the fly) asynchronously configuration object define করা যায়।

বিকল্পভাবে, `create()` method এর options object এর মাধ্যমেও CORS enable করা যায়। Default setting দিয়ে CORS enable করতে `cors` property কে `true` সেট করো।
অথবা, এর behavior customize করতে `cors` property এর value হিসেবে একটা [CORS configuration object](https://github.com/expressjs/cors#configuration-options) বা [callback function](https://github.com/expressjs/cors#configuring-cors-asynchronously) পাস করো।

```typescript
const app = await NestFactory.create(AppModule, { cors: true });
await app.listen(process.env.PORT ?? 3000);
```
