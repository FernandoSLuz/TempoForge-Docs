# Editor tools

5 types in this area.

!!! abstract "On this page"
    [AuthoringMigrationBatchOrchestrator](#authoringmigrationbatchorchestrator) &middot; [AuthoringMigrationRegistry](#authoringmigrationregistry) &middot; [BattleSkinBrowserWindow](#battleskinbrowserwindow) &middot; [IAuthoringAssetMigration](#iauthoringassetmigration) &middot; [IAuthoringStableIdChangingMigration](#iauthoringstableidchangingmigration)

## AuthoringMigrationBatchOrchestrator

```csharp
public sealed class AuthoringMigrationBatchOrchestrator
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Validation/Migrations/AuthoringMigrationBatchOrchestrator.cs</small>

Explicit, synchronous Editor migration transaction. It never discovers
assets, saves assets, or runs from import/deserialization callbacks.

**Constructors**

`public AuthoringMigrationBatchOrchestrator()`

:   &mdash;

`public AuthoringMigrationBatchOrchestrator()`

:   &mdash;

**Methods**

`public MigrationBatchResult MigrateAffectedClosure()`

:   &mdash;

---

## AuthoringMigrationRegistry

```csharp
public sealed class AuthoringMigrationRegistry
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

The ordered list of migration steps a batch run will apply.

Steps are listed explicitly and in version order; there is no reflection
discovery, so a migration cannot appear in a run because it happened to be
compiled into the project. That is deliberate - content migrations rewrite
a buyer's assets, and the set that runs has to be the set someone chose.

`Product` holds the shipped steps and is currently empty,
schema 1 being the first public schema with nothing to migrate from. Build
your own instance to run your own steps.

**Constructors**

`public AuthoringMigrationRegistry()`

:   &mdash;

**Properties**

`public FrozenList<IAuthoringAssetMigration> OrderedSteps`

:   &mdash;

`public static AuthoringMigrationRegistry Product`

:   &mdash;

---

## BattleSkinBrowserWindow

```csharp
public sealed class BattleSkinBrowserWindow : EditorWindow
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Skins/BattleSkinBrowserWindow.cs</small>

Browse the shipped skins, preview them with the real shader, and turn any
of them into an editable asset in one click.

This window exists because the package previously offered no way to
discover or create a look: a customer had to create a blank asset and fill
in fields with no preview. "Create editable copy" is the intended entry
point for authoring a custom skin.

**Fields**

`public BattleSkinPreset Asset`

:   The asset this entry was loaded from, or null for a shipped skin. The actions that need a file on disk are disabled while it is null.

`public bool IsShipped`

:   Whether the look is defined in package code rather than by an asset. Shipped entries are listed first and cannot be edited in place, which is what `Create editable copy` is for.

`public CompiledBattleSkin Skin`

:   The compiled look this row previews. For a project asset it is a compile of that asset taken at refresh time, so an edit made elsewhere appears once the window regains focus, not before.

**Methods**

`public static void Open()`

:   Opens the skin browser, or brings it forward when it is already open. Also reachable from Tools > TempoForge > Skin Browser.

`public void Refresh()`

:   Rebuilds the list from shipped skins plus project assets.

---

## IAuthoringAssetMigration

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IAuthoringAssetMigration
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

One step that upgrades authored assets from one schema version to the next.

This is the seam for a project's own content migrations: implement it, pass
the steps to a new `AuthoringMigrationRegistry`, and run them
through `AuthoringMigrationBatchOrchestrator`. The shipped menu
commands always use the product registry, so your steps run only from your
own editor code and can never fire behind your back.

A step that needs to change a `StableIdRaw` must also implement
`IAuthoringStableIdChangingMigration`; without it the change is
rejected, because a silently rewritten identity is unrecoverable.

---

## IAuthoringStableIdChangingMigration

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IAuthoringStableIdChangingMigration
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

Optional, deliberately conspicuous escape hatch for a future documented
public migration that must change gameplay identity. Ordinary migrations
are rejected if they alter StableIdRaw.

---

