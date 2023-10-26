# ngrxStore

J'essaie de créer un code simple avec un store simple : 

On a un utilisateur (dans user.reducer.ts) de la forme : 
``export interface UserState {
  name: string;
  age: number;
}
``

J'ai mes actions (user.actions.ts): 

```
export const changeUserName = createAction(
  '[User] Change Name',
  props<{ newName: string }>()
);

export const changeUserAge = createAction(
  '[User] Change Age',
  props<{ newAge: number }>()
);
```
J'ai mes selecteurs (user.selector.ts): 

```
export const selectUserState = createFeatureSelector<UserState>('user');

export const selectUserName = createSelector(
  selectUserState,
  (state) => state.name
);

export const selectUserAge = createSelector(
  selectUserState,
  (state) => state.age
);

```

J'ai bien déclarer mon Store dans mon module app.module.ts : 

```
 imports: [
    BrowserModule,
    AppRoutingModule,
    StoreModule.forRoot({
      user: userReducer
    })
  ],

```

Dans mon AppComponent j'essaie de récupérer les valeurs de userName et userAge du store et ensuite de changer le nom et l'age : 

```
userName$ = this.store.select(selectUserName);
userAge$ = this.store.select(selectUserAge);
```

```
changeUserName(newName: string) {
  this.store.dispatch(changeUserName({ newName }));
}

changeUserAge(newAge: number) {
  this.store.dispatch(changeUserAge({ newAge }));
}
```

Tout compile et je n'ai pas d'erreur dans mon code mais lorsque je me mets sur L'URL la console me sort cette erreur (sur FireFox et Chrome) : 

![image](https://github.com/DamsRob/ngrxStore/assets/148881811/f60fd971-e9ec-4f96-bb71-ae67a1b7f14f)

  
