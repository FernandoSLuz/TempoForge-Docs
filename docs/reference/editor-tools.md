# Editor tools

8 types in this area.

!!! abstract "On this page"
    [AuthoringMigrationBatchOrchestrator](#authoringmigrationbatchorchestrator) &middot; [AuthoringMigrationRegistry](#authoringmigrationregistry) &middot; [BattleSkinBrowserWindow](#battleskinbrowserwindow) &middot; [BattleTemplateBrowserWindow](#battletemplatebrowserwindow) &middot; [CloneResult](#cloneresult) &middot; [IAuthoringAssetMigration](#iauthoringassetmigration) &middot; [IAuthoringStableIdChangingMigration](#iauthoringstableidchangingmigration) &middot; [StarterContentCloner](#startercontentcloner)

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

## BattleTemplateBrowserWindow

```csharp
public sealed class BattleTemplateBrowserWindow : EditorWindow
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Templates/BattleTemplateBrowserWindow.cs</small>

Browse the shipped battle templates, see the stage each one lays out, and
turn any of them into real authoring assets in one click.

This window is the answer to "I imported the package, now what". Before it,
the two ways to start were an empty catalog - which compiles to nothing until
a dozen assets exist - or hand-copying the samples, which a package reimport
then overwrites. Both are still available; this is the one that leaves you
with content you own.

**Methods**

`public static void Open()`

:   Opens the browser, focusing an existing window if one is open.

---

## CloneResult

```csharp
public sealed class CloneResult
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Templates/StarterContentCloner.cs</small>

What one clone produced: the catalog you now own, what was written, what
was deliberately left alone, and what the compiler made of the result.

**Properties**

`public BattleContentCatalog Catalog`

:   The cloned catalog root, already saved and importable.

`public bool Compiled`

:   Whether the clone compiled. False leaves the written assets in place deliberately, so the failure can be inspected rather than guessed at.

`public IReadOnlyList<string> CreatedPaths`

:   Every asset path written, in the order they were created.

`public IReadOnlyList<AuthoringDiagnostic> Diagnostics`

:   What the compiler said about the clone. Empty on a clean clone; a dangling reference here means a reference this tool did not follow.

`public IReadOnlyList<string> KeptIdentities`

:   Identities that were deliberately not renamed because they resolve in a registry, so they name a contract rather than a piece of content. An empty list is unusual: a catalog names at least one scheduler.

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

## StarterContentCloner

```csharp
public static class StarterContentCloner
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Templates/StarterContentCloner.cs</small>

Copies a shipped catalog into a folder of your own and gives the copies
fresh identities, so the starter content becomes a starting point you can
edit rather than a package file that a reimport overwrites.

Renaming identities across a copied asset graph is where this kind of tool
goes wrong quietly, so three rules are worth stating outright.

First, a stable ID is not always content. Two of them - the built-in
scheduler IDs - are keys the compiler looks up in the scheduler registry, so
renaming them would leave the definition unresolvable rather than merely
renamed. Any ID that resolves in either registry is kept as it stands and
reported in `CloneResult.KeptIdentities`.

Second, not every reference between definitions is an object reference. A
property bag can hold a stable ID as text - the shipped damage effect names
`stat.power` that way - and renaming the stat asset without rewriting
that text would leave a formula pointing at a stat the cloned catalog no
longer contains. Those texts are rewritten, and only when they match the ID
of an asset actually being cloned, which is what keeps a registry key such as
`formula.standard-damage.v1` untouched.

Third, none of the above is trusted. The clone is compiled before this
returns, and `CloneResult.Diagnostics` carries whatever the
compiler said. A reference this tool failed to follow does not stay hidden:
it becomes a dangling reference in a catalog that no longer contains the
original, and the compile reports it.

---

