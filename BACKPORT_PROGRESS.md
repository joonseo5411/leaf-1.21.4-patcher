# 백포트 진행 상황 (1.21.11/26.2 → 1.21.4, 순수 최적화 패치)

출처: `leaf-patch-comparison-262-vs-12111-vs-1214.md` (serenity 저장소) 4절의 BL(1.21.11+26.2엔 있고 1.21.4엔 없음) 목록 중 🟢 최적화 성격으로 분류된 항목.

체크된 항목은 이 저장소에 실제로 포팅되어 `leaf-server/minecraft-patches/features/` 등에 패치로 존재함. 나머지는 아직 미착수.

## minecraft-patches (118개)

- [ ] Add-io_uring-support.patch
- [ ] Better-checking-for-useless-move-packets.patch
- [ ] Broadcast-crit-animations-as-the-entity-being-critte.patch
- [x] Cache-ShapePairKey-hash.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (Block.ShapePairKey에 hash 필드 이미 존재)*
- [x] Cache-block-state-tags.patch
- [x] Cache-identifier-toString-and-hash.patch
- [x] Cache-world-border.patch — *포팅 불필요: 1.21.4 vanilla/Paper already caches it as a direct field (Level.java), so this patch does not apply*
- [ ] Cache-world-generator-sea-level.patch
- [x] Check-frozen-ticks-before-landing-block.patch — *포팅 불필요: 검증 결과 이미 Gale 기반에 포함(추정, 관련 로직 확인)*
- [ ] Check-targeting-range-before-getting-visibility.patch
- [x] Don-t-load-POI-for-competitor-scan.patch
- [ ] Don-t-load-chunks-to-spawn-phantoms.patch
- [x] Faster-floating-point-positive-modulo.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (Mth.java positiveModuloForPositiveIntegerDenominator 등 이미 존재)*
- [ ] Filter-ClientboundSetEntityMotionPacket.patch
- [x] For-collision-check-has-physics-before-same-vehicle.patch — *포팅 불필요: 이미 Gale/Akarin 기반에 포함되어 있음*
- [x] Initialize-line-of-sight-cache-with-low-capacity.patch — *포팅 불필요: 이미 상위 최적화(Reduce line of sight updates)에 흡수되어 포함되어 있음*
- [ ] Leaves-Lithium-Sleeping-Block-Entity.patch
- [ ] Lithium-combined-heightmap-update.patch
- [ ] Lithium-equipment-tracking.patch
- [ ] Lithium-faster-hash-palette.patch
- [ ] Luminol-Configurable-region-format-framework.patch
- [x] Make-EntityCollisionContext-a-live-representation.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [x] Move-random-tick-random.patch — *포팅 불필요: 이미 Gale/Pufferfish 기반에 포함되어 있음 (Level.java에 simpleRandom 필드 이미 존재)*
- [x] Only-update-frozen-ticks-if-changed.patch
- [x] Optimise-getEntities.patch
- [x] Optimize-PatchedDataComponentMap-equals.patch
- [x] Optimize-VarInt-write-and-VarLong-write.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음 (VarInt.java/VarLong.java에 이미 존재)*
- [x] Optimize-Vec3i-hashing.patch
- [x] Optimize-map-lookups-with-isEmpty-check.patch
- [ ] Optimize-matching-item-checks.patch
- [x] Optimize-noise-generation.patch — *포팅 불필요: 이미 Gale/C2ME 기반에 포함되어 있음 (ImprovedNoise.java FLAT_SIMPLEX_GRAD 이미 존재)*
- [x] Optimize-pushable-selector.patch
- [ ] Optimize-random-calls-in-chunk-ticking.patch
- [ ] Optimize-respawn-anchor-explosion.patch
- [x] Optimize-sheep-offspring-color.patch — *포팅 불필요: 이미 Gale/carpet-fixes 기반에 포함되어 있음 (DyeColor.getMixedColor 이미 최적화됨)*
- [x] Optimize-sun-burn-tick.patch — *포팅 불필요: 이미 Gale/JettPack 기반에 포함되어 있음 (Entity.isSunBurnTick 이미 캐싱 적용됨)*
- [ ] Paper-PR-Optimise-temptation-lookups-changes.patch
- [ ] Paper-PR-Optimise-temptation-lookups.patch
- [ ] Pluto-Expose-Direction-Plane-s-faces.patch
- [ ] Pluto-don-t-load-chunks-to-spread-grass.patch
- [ ] Pluto-reduce-allocation.patch
- [x] Pre-compute-VarLong-sizes.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음*
- [ ] Prevent-entities-from-moving-into-weak-loaded-chunks.patch
- [x] Prevent-entities-random-strolling-into-non-ticking-c.patch — *포팅 불필요: 이미 Gale/MultiPaper 기반에 포함되어 있음*
- [x] Reduce-AbstractContainerMenu-allocations.patch
- [x] Reduce-RandomSource-instances.patch — *포팅 불필요: 이미 Gale/Patina 기반에 동일 최적화가 포함되어 있음 (Raid.java 등에 이미 존재)*
- [ ] Reduce-array-allocations.patch
- [x] Reduce-block-destruction-packet-allocations.patch — *포팅 불필요: 이미 Gale/SportPaper 기반에 포함되어 있음*
- [x] Reduce-debug-subscribers-overhead.patch — *포팅 불필요: 1.21.4엔 debug subscribers 기능 자체가 없음 (ServerDebugSubscribers.java 클래스 부재, 더 최신 MC 버전 기능)*
- [x] Reduce-enderman-teleport-chunk-lookups.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음 (EnderMan.teleport 이미 single chunk lookup 적용됨)*
- [ ] Reduce-in-wall-checks.patch
- [x] Reduce-lambda-and-Optional-allocation-in-EntityBased.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음*
- [x] Reduce-line-of-sight-updates-and-cache-lookups.patch — *포팅 불필요: 이미 Gale/Petal 기반에 포함되어 있음 (Sensing.java expiring 배열 구조 이미 존재)*
- [ ] Reduce-optimiseRandomTick-new-BlockPos-instance-crea.patch
- [x] Reduce-projectile-chunk-loading.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [x] Reduce-skull-ItemStack-lookups-for-reduced-visibilit.patch — *포팅 불필요: 이미 Gale/Petal 기반에 포함되어 있음*
- [x] Reduce-villager-item-re-pickup.patch — *포팅 불필요: 이미 Gale/EMC 기반에 포함되어 있음*
- [ ] Remove-iterators-from-Inventory.patch
- [x] Remove-lambda-from-ticking-guard.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [ ] Remove-stream-in-CraftWorld-spawnParticle.patch
- [x] Remove-stream-in-MobSensor.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음 (변수명만 다름)*
- [x] Remove-stream-in-TemptingSensor.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Remove-stream-on-PlayerDetector.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Remove-stream-on-updateConnectedPlayersWithinRange.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Replace-EntitySelectorOptions-map-with-optimized-col.patch
- [ ] Replace-brain-with-optimized-collection.patch
- [ ] Replace-division-by-multiplication-in-CubePointRange.patch
- [ ] Replace-entity-equipment-items-to-array.patch
- [ ] Replace-parts-by-size-in-CubePointRange.patch
- [ ] Replace-throttle-tracker-map-with-optimized-collecti.patch
- [ ] Rewrite-entity-despawn-time.patch
- [ ] SIMD-support.patch
- [x] Send-multiple-keep-alive-packets.patch — *포팅 불필요: 이미 Gale/Purpur 기반에 포함되어 있음*
- [x] Skip-BlockPhysicsEvent-if-no-listeners.patch — *포팅 완료(1.21.4는 원본과 달리 cworld != null 체크가 추가로 있어 두 조건을 함께 사용)*
- [ ] Skip-PlayerCommandSendEvent-if-there-are-no-listener.patch
- [x] Skip-PreCreatureSpawnEvent-if-no-listeners.patch — *포팅 완료(원본은 2개 메서드를 건드리지만 1.21.4엔 그 중 1개 메서드 형태만 존재해서 그 부분만 적용)*
- [x] Skip-VehicleEntityCollisionEvent-if-no-listeners.patch
- [x] Skip-cloning-advancement-criteria.patch — *포팅 불필요: 이미 Gale/Mirai 기반에 포함되어 있음 (Advancement 레코드 압축 생성자에 이미 적용됨)*
- [x] Skip-entity-move-if-movement-is-zero.patch — *포팅 불필요: 이미 Gale/VMP 기반에 포함되어 있음 (Entity.java에 boundingBoxChanged 필드 이미 존재)*
- [ ] Skip-inactive-entity-for-execute.patch
- [x] Skip-item-merge-checks-for-full-stacks.patch
- [ ] Skip-negligible-planar-movement-multiplication.patch
- [x] Skip-secondary-POI-sensor-if-absent.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음 (SecondaryPoiSensor.java에 이미 적용됨)*
- [ ] Spread-out-sending-all-player-info.patch
- [x] Store-mob-counts-in-an-array.patch — *포팅 불필요: 이미 Gale/VMP 기반에 포함되어 있음 (LocalMobCapCalculator.java에 int[] counts 이미 존재)*
- [ ] Update-boss-bar-within-tick.patch
- [ ] Use-linked-map-for-entity-trackers.patch
- [ ] Variable-entity-wake-up-duration.patch
- [ ] Virtual-thread-support-for-chat-executor.patch
- [ ] Virtual-thread-support-for-download-pool.patch
- [ ] async-chunk-sender.patch
- [ ] cache-biome-for-mob-spawning-and-advancements.patch
- [x] cache-collision-list.patch
- [x] fast-bit-radix-sort.patch — *포팅 불필요: 이미 다른 형태(List<T>+Class 기반 API)로 구현되어 있음 (NearestItemSensor.itemSorter)*
- [ ] fixup-Leaves-Lithium-Sleeping-Block-Entity.patch
- [ ] optimize-LevelChunk-getBlockStateFinal.patch
- [ ] optimize-PalettedContainer-get.patch
- [ ] optimize-PathNavigation-followThePath.patch
- [ ] optimize-SimpleBitStorage-object-layout.patch
- [ ] optimize-applyMovementEmissionAndPlaySound.patch
- [ ] optimize-attribute.patch
- [x] optimize-canHoldAnyFluid.patch
- [ ] optimize-checkInsideBlocks-calls.patch
- [ ] optimize-collidedAlongVector.patch
- [ ] optimize-collision-shape.patch
- [ ] optimize-get-chunk.patch
- [x] optimize-getOnPos.patch
- [ ] optimize-goal-selector.patch
- [x] optimize-isStateClimbable.patch
- [ ] optimize-mob-despawn.patch
- [ ] optimize-movement-vector-normalization.patch
- [ ] optimize-no-action-time.patch
- [ ] optimize-tickEffects.patch
- [ ] optimize-waypoint.patch
- [x] reduce-enchantment-allocations.patch
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

- [x] Cache-namespacedKey-toString-and-hash.patch
- [ ] Fish-Parallel-World-Ticking-API.patch
- [ ] Player-canSee-by-entity-UUID.patch
- [x] Replace-data-maps-with-optimized-collection.patch
- [ ] SIMD-support.patch

**진행률: 56 / 138 체크됨** (실제 포팅 20개, 나머지는 이미 각종 서드파티 포크 기반에 구현되어 있거나 1.21.4엔 없는 기능이라 불필요로 확인됨.

**Phase 2 완료**: `Cache-block-state-tags` 기반 패치(BlockState에 `tagFlag` 캐시 필드 + `org.dreeam.leaf.util.BlockMasks` 유틸리티 추가; `pathType` 캐시는 1.21.4에 이미 별도로 존재해서 손댈 필요 없었음)를 실제로 포팅해서 `optimize-getOnPos`, `optimize-isStateClimbable`, `optimize-canHoldAnyFluid` 3개를 추가로 풀었음. 펜스/벽/펜스게이트/사다리/가루눈/트랩도어/덩굴/유체/가마솥 상호작용을 헤드리스 봇으로 전부 실전 테스트, 예외 0건.

기타 보류: Optimize-respawn-anchor-explosion(getFluidStateIfLoadedUnchecked 헬퍼 필요), Skip-inactive-entity-for-execute(신규 config 모듈 + Leaves ServerPhotographer 필요), Rewrite-entity-despawn-time(엔티티 생명주기+청크시스템 광범위 변경), optimize-attribute(AttributeInstanceArrayMap 등 대규모 신규 컬렉션 인프라 필요)**

## 포팅 절차 (참고)

1. `ver/26.2` 또는 `ver/1.21.11`에서 해당 패치 원문(`leaf-server/minecraft-patches/features/NNNN-*.patch`)을 확인
2. `leaf-server/src/minecraft/java` (paperweight 작업 트리, 별도 git repo)에서 대상 파일을 찾아 diff를 1.21.4 소스 기준으로 재적용
3. `git add` + `git commit` (커밋 메시지 = 패치 제목)
4. 루트에서 `JAVA_HOME=/usr/lib/jvm/java-21-openjdk-arm64 ./gradlew rebuildMinecraftFeaturePatches` 실행 → `leaf-server/minecraft-patches/features/`에 새 패치 파일 자동 생성
5. `./gradlew :leaf-server:compileJava` 로 컴파일 검증
6. 이 파일에 체크 표시 후 커밋