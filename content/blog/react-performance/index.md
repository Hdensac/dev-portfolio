---
title: "Optimiser les performances React : guide pratique"
date: 2024-11-22
summary: "Méthodes concrètes pour identifier les ralentissements dans une application React et appliquer les bonnes optimisations."
tags:
  - React
  - Performance
  - JavaScript
  - Frontend
  - Optimisation
authors:
  - me
featured: true
---

Une application React peut devenir lente lorsque les composants, les états et les listes grossissent. Avant d'optimiser, il faut mesurer : le Profiler de React DevTools permet de repérer les composants qui se rendent trop souvent ou trop lentement.

## Problèmes fréquents

- Rendus inutiles de composants enfants
- Calculs coûteux exécutés à chaque rendu
- Listes trop grandes affichées entièrement
- Contexte global qui force trop de composants à se mettre à jour
- Bundle initial trop lourd

## Éviter les rendus inutiles

`React.memo` est utile pour les composants qui reçoivent rarement de nouvelles propriétés mais qui sont rendus souvent par leur parent.

```jsx
const ExpensiveChild = React.memo(() => {
  return <div>{/* rendu coûteux */}</div>
})
```

Cette optimisation doit être utilisée après mesure. La mémorisation systématique peut rendre le code plus complexe sans gain réel.

## Mémoriser les calculs coûteux

`useMemo` évite de recalculer une valeur quand ses dépendances n'ont pas changé.

```jsx
function ProductList({ products, searchTerm }) {
  const filtered = useMemo(() =>
    products.filter((product) =>
      product.name.toLowerCase().includes(searchTerm.toLowerCase())
    ),
    [products, searchTerm]
  )

  return <ul>{filtered.map((product) => <li key={product.id}>{product.name}</li>)}</ul>
}
```

## Stabiliser les callbacks

`useCallback` est utile quand une fonction est transmise à un composant mémorisé.

```jsx
const handleClick = useCallback(() => {
  setCount((count) => count + 1)
}, [])
```

## Virtualiser les grandes listes

Pour des milliers d'éléments, afficher uniquement les lignes visibles améliore fortement la fluidité. Des bibliothèques comme `react-window` sont faites pour ce cas.

## Découper le code

`React.lazy` et `Suspense` permettent de charger certaines parties de l'application seulement quand elles sont nécessaires.

```jsx
const AdminPanel = React.lazy(() => import('./AdminPanel'))
```

Le résultat est un bundle initial plus léger et un premier affichage plus rapide.

## Checklist performance

- Mesurer avec React DevTools Profiler
- Optimiser les composants réellement coûteux
- Utiliser `useMemo` pour les calculs lourds
- Utiliser `useCallback` pour les callbacks transmis à des composants mémorisés
- Virtualiser les très grandes listes
- Découper les pages ou modules volumineux
- Utiliser des clés stables dans les listes
- Séparer les contextes trop larges

## Conclusion

La performance React n'est pas une question de réflexes automatiques. La bonne approche consiste à mesurer, identifier le vrai goulot d'étranglement, appliquer une optimisation ciblée, puis vérifier le résultat.
