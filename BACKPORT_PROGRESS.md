# 백포트 진행 상황 (1.21.11/26.2 → 1.21.4, 순수 최적화 패치)

출처: `leaf-patch-comparison-262-vs-12111-vs-1214.md` (serenity 저장소) 4절의 BL(1.21.11+26.2엔 있고 1.21.4엔 없음) 목록 중 🟢 최적화 성격으로 분류된 항목.

체크된 항목은 이 저장소에 실제로 포팅되어 `leaf-server/minecraft-patches/features/` 등에 패치로 존재함. 나머지는 아직 미착수.

## minecraft-patches (118개)

- [ ] Add-io_uring-support.patch
- [ ] Better-checking-for-useless-move-packets.patch
- [ ] Broadcast-crit-animations-as-the-entity-being-critte.patch
- [ ] Cache-ShapePairKey-hash.patch
- [ ] Cache-block-state-tags.patch
- [x] Cache-identifier-toString-and-hash.patch
- [x] Cache-world-border.patch — *포팅 불필요: 1.21.4 vanilla/Paper already caches it as a direct field (Level.java), so this patch does not apply*
- [ ] Cache-world-generator-sea-level.patch
- [ ] Check-frozen-ticks-before-landing-block.patch
- [ ] Check-targeting-range-before-getting-visibility.patch
- [ ] Don-t-load-POI-for-competitor-scan.patch
- [ ] Don-t-load-chunks-to-spawn-phantoms.patch
- [ ] Faster-floating-point-positive-modulo.patch
- [ ] Filter-ClientboundSetEntityMotionPacket.patch
- [ ] For-collision-check-has-physics-before-same-vehicle.patch
- [ ] Initialize-line-of-sight-cache-with-low-capacity.patch
- [ ] Leaves-Lithium-Sleeping-Block-Entity.patch
- [ ] Lithium-combined-heightmap-update.patch
- [ ] Lithium-equipment-tracking.patch
- [ ] Lithium-faster-hash-palette.patch
- [ ] Luminol-Configurable-region-format-framework.patch
- [ ] Make-EntityCollisionContext-a-live-representation.patch
- [ ] Move-random-tick-random.patch
- [ ] Only-update-frozen-ticks-if-changed.patch
- [ ] Optimise-getEntities.patch
- [ ] Optimize-PatchedDataComponentMap-equals.patch
- [x] Optimize-VarInt-write-and-VarLong-write.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음 (VarInt.java/VarLong.java에 이미 존재)*
- [x] Optimize-Vec3i-hashing.patch
- [x] Optimize-map-lookups-with-isEmpty-check.patch
- [ ] Optimize-matching-item-checks.patch
- [ ] Optimize-noise-generation.patch
- [ ] Optimize-pushable-selector.patch
- [ ] Optimize-random-calls-in-chunk-ticking.patch
- [ ] Optimize-respawn-anchor-explosion.patch
- [ ] Optimize-sheep-offspring-color.patch
- [ ] Optimize-sun-burn-tick.patch
- [ ] Paper-PR-Optimise-temptation-lookups-changes.patch
- [ ] Paper-PR-Optimise-temptation-lookups.patch
- [ ] Pluto-Expose-Direction-Plane-s-faces.patch
- [ ] Pluto-don-t-load-chunks-to-spread-grass.patch
- [ ] Pluto-reduce-allocation.patch
- [x] Pre-compute-VarLong-sizes.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음*
- [ ] Prevent-entities-from-moving-into-weak-loaded-chunks.patch
- [ ] Prevent-entities-random-strolling-into-non-ticking-c.patch
- [ ] Reduce-AbstractContainerMenu-allocations.patch
- [x] Reduce-RandomSource-instances.patch — *포팅 불필요: 이미 Gale/Patina 기반에 동일 최적화가 포함되어 있음 (Raid.java 등에 이미 존재)*
- [ ] Reduce-array-allocations.patch
- [ ] Reduce-block-destruction-packet-allocations.patch
- [ ] Reduce-debug-subscribers-overhead.patch
- [ ] Reduce-enderman-teleport-chunk-lookups.patch
- [ ] Reduce-in-wall-checks.patch
- [ ] Reduce-lambda-and-Optional-allocation-in-EntityBased.patch
- [ ] Reduce-line-of-sight-updates-and-cache-lookups.patch
- [ ] Reduce-optimiseRandomTick-new-BlockPos-instance-crea.patch
- [ ] Reduce-projectile-chunk-loading.patch
- [ ] Reduce-skull-ItemStack-lookups-for-reduced-visibilit.patch
- [ ] Reduce-villager-item-re-pickup.patch
- [ ] Remove-iterators-from-Inventory.patch
- [ ] Remove-lambda-from-ticking-guard.patch
- [ ] Remove-stream-in-CraftWorld-spawnParticle.patch
- [ ] Remove-stream-in-MobSensor.patch
- [ ] Remove-stream-in-TemptingSensor.patch
- [ ] Remove-stream-on-PlayerDetector.patch
- [ ] Remove-stream-on-updateConnectedPlayersWithinRange.patch
- [ ] Replace-EntitySelectorOptions-map-with-optimized-col.patch
- [ ] Replace-brain-with-optimized-collection.patch
- [ ] Replace-division-by-multiplication-in-CubePointRange.patch
- [ ] Replace-entity-equipment-items-to-array.patch
- [ ] Replace-parts-by-size-in-CubePointRange.patch
- [ ] Replace-throttle-tracker-map-with-optimized-collecti.patch
- [ ] Rewrite-entity-despawn-time.patch
- [ ] SIMD-support.patch
- [ ] Send-multiple-keep-alive-packets.patch
- [ ] Skip-BlockPhysicsEvent-if-no-listeners.patch
- [ ] Skip-PlayerCommandSendEvent-if-there-are-no-listener.patch
- [ ] Skip-PreCreatureSpawnEvent-if-no-listeners.patch
- [ ] Skip-VehicleEntityCollisionEvent-if-no-listeners.patch
- [ ] Skip-cloning-advancement-criteria.patch
- [ ] Skip-entity-move-if-movement-is-zero.patch
- [ ] Skip-inactive-entity-for-execute.patch
- [ ] Skip-item-merge-checks-for-full-stacks.patch
- [ ] Skip-negligible-planar-movement-multiplication.patch
- [ ] Skip-secondary-POI-sensor-if-absent.patch
- [ ] Spread-out-sending-all-player-info.patch
- [ ] Store-mob-counts-in-an-array.patch
- [ ] Update-boss-bar-within-tick.patch
- [ ] Use-linked-map-for-entity-trackers.patch
- [ ] Variable-entity-wake-up-duration.patch
- [ ] Virtual-thread-support-for-chat-executor.patch
- [ ] Virtual-thread-support-for-download-pool.patch
- [ ] async-chunk-sender.patch
- [ ] cache-biome-for-mob-spawning-and-advancements.patch
- [ ] cache-collision-list.patch
- [ ] fast-bit-radix-sort.patch
- [ ] fixup-Leaves-Lithium-Sleeping-Block-Entity.patch
- [ ] optimize-LevelChunk-getBlockStateFinal.patch
- [ ] optimize-PalettedContainer-get.patch
- [ ] optimize-PathNavigation-followThePath.patch
- [ ] optimize-SimpleBitStorage-object-layout.patch
- [ ] optimize-applyMovementEmissionAndPlaySound.patch
- [ ] optimize-attribute.patch
- [ ] optimize-canHoldAnyFluid.patch
- [ ] optimize-checkInsideBlocks-calls.patch
- [ ] optimize-collidedAlongVector.patch
- [ ] optimize-collision-shape.patch
- [ ] optimize-get-chunk.patch
- [ ] optimize-getOnPos.patch
- [ ] optimize-goal-selector.patch
- [ ] optimize-isStateClimbable.patch
- [ ] optimize-mob-despawn.patch
- [ ] optimize-movement-vector-normalization.patch
- [ ] optimize-no-action-time.patch
- [ ] optimize-tickEffects.patch
- [ ] optimize-waypoint.patch
- [ ] reduce-enchantment-allocations.patch
- [ ] remove-shouldTickBlocksAt-check.patch
- [ ] rewrite-InsideBrownianWalk.patch
- [ ] thread-unsafe-chunk-map.patch

## paper-patches (15개)

- [ ] Fish-Parallel-World-Ticking-API.patch
- [ ] Leaf-Test-Async-Executor.patch
- [x] Optimize-VarInt-write-and-VarLong-write.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음 (VarInt.java/VarLong.java에 이미 존재)*
- [ ] Optimize-block-entities-count.patch
- [x] Pre-compute-VarLong-sizes.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음*
- [ ] Reduce-array-allocations.patch
- [ ] Remove-stream-in-CraftWorld-spawnParticle.patch
- [ ] SIMD-support.patch
- [ ] Use-optimized-collections-in-CB-classes.patch
- [ ] Virtual-thread-support-for-bukkit-async-scheduler.patch
- [ ] Virtual-thread-support-for-chat-executor.patch
- [ ] Virtual-thread-support-for-folia-async-scheduler.patch
- [ ] Virtual-thread-support.patch
- [ ] optimize-despawn.patch
- [ ] optimize-mob-spawning.patch

## leaf-api (5개)

- [ ] Cache-namespacedKey-toString-and-hash.patch
- [ ] Fish-Parallel-World-Ticking-API.patch
- [ ] Player-canSee-by-entity-UUID.patch
- [ ] Replace-data-maps-with-optimized-collection.patch
- [ ] SIMD-support.patch

**진행률: 9 / 138 체크됨** (고유 패치 기준 7개: 실제 포팅 3개 — Vec3i hashing, Cache identifier toString/hash, Optimize map lookups with isEmpty check / 이미 Gale·Patina 기반에 구현되어 있어 포팅 불필요로 확인 4개 — Cache world border, Optimize VarInt-VarLong write, Pre-compute VarLong sizes, Reduce RandomSource instances. 일부는 minecraft-patches·paper-patches 두 섹션에 동시 등장해 체크 줄 수는 9줄)

## 포팅 절차 (참고)

1. `ver/26.2` 또는 `ver/1.21.11`에서 해당 패치 원문(`leaf-server/minecraft-patches/features/NNNN-*.patch`)을 확인
2. `leaf-server/src/minecraft/java` (paperweight 작업 트리, 별도 git repo)에서 대상 파일을 찾아 diff를 1.21.4 소스 기준으로 재적용
3. `git add` + `git commit` (커밋 메시지 = 패치 제목)
4. 루트에서 `JAVA_HOME=/usr/lib/jvm/java-21-openjdk-arm64 ./gradlew rebuildMinecraftFeaturePatches` 실행 → `leaf-server/minecraft-patches/features/`에 새 패치 파일 자동 생성
5. `./gradlew :leaf-server:compileJava` 로 컴파일 검증
6. 이 파일에 체크 표시 후 커밋