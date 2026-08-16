# 백포트 진행 상황 (1.21.11/26.2 → 1.21.4, 순수 최적화 패치)

출처: `leaf-patch-comparison-262-vs-12111-vs-1214.md` (serenity 저장소) 4절의 BL(1.21.11+26.2엔 있고 1.21.4엔 없음) 목록 중 🟢 최적화 성격으로 분류된 항목.

체크된 항목은 이 저장소에 실제로 포팅되어 `leaf-server/minecraft-patches/features/` 등에 패치로 존재함. 나머지는 아직 미착수.

## minecraft-patches (118개)

- [ ] Add-io_uring-support.patch — *보류: 대상 클래스 io/netty 채널 선택 추상화(EventLoopGroupHolder.java)가 1.21.4엔 없음 — 1.21.4는 ServerConnectionListener.java 안에서 NIO/Epoll만 직접 분기하는 더 단순한 구조라 io_uring을 붙이려면 핵심 네트워크 부트스트랩 코드를 직접 건드려야 함(전체 접속 수락 로직 리스크). netty-incubator-transport-native-io_uring:0.0.26.Final 의존성(linux-x86_64/aarch_64 클래시파이어 확인됨)까지는 준비했으나 실제 코드 포팅은 리스크 대비 이득이 낮아 보류, 전용 세션 권장*
- [x] Better-checking-for-useless-move-packets.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음 (ServerEntity.java에 이미 적용됨)*
- [ ] Broadcast-crit-animations-as-the-entity-being-critte.patch — *범위 밖: 순수 최적화가 아닌 gameplay/네트워킹 가시성 수정(공격자가 근처 플레이어에게 트래킹 안 될 때 크리티컬 애니메이션이 안 보이는 문제) + 신규 config 필드 필요, 최적화 백포트 범위에서 제외*
- [x] Cache-ShapePairKey-hash.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (Block.ShapePairKey에 hash 필드 이미 존재)*
- [x] Cache-block-state-tags.patch
- [x] Cache-identifier-toString-and-hash.patch
- [x] Cache-world-border.patch — *포팅 불필요: 1.21.4 vanilla/Paper already caches it as a direct field (Level.java), so this patch does not apply*
- [x] Cache-world-generator-sea-level.patch
- [x] Check-frozen-ticks-before-landing-block.patch — *포팅 불필요: 검증 결과 이미 Gale 기반에 포함(추정, 관련 로직 확인)*
- [x] Check-targeting-range-before-getting-visibility.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음 (TargetingConditions.java에 followRangeRaw 조기 return 이미 존재)*
- [x] Don-t-load-POI-for-competitor-scan.patch
- [x] Don-t-load-chunks-to-spawn-phantoms.patch — *포팅 불필요: 이미 Gale/MultiPaper 기반에 포함되어 있음 (PhantomSpawner.java에 galeConfig().smallOptimizations.loadChunks.toSpawnPhantoms 이미 존재)*
- [x] Faster-floating-point-positive-modulo.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (Mth.java positiveModuloForPositiveIntegerDenominator 등 이미 존재)*
- [x] Filter-ClientboundSetEntityMotionPacket.patch — *포팅 완료(기본값 false로 기존 동작 유지). 기존 ReduceUselessPackets config 모듈에 filterClientboundSetEntityMotionPacket 필드 추가 + ServerEntity.java 1곳(1.21.4엔 Folia 전용 두번째 tracker 경로 없어 1곳만 존재)에 적용*
- [x] For-collision-check-has-physics-before-same-vehicle.patch — *포팅 불필요: 이미 Gale/Akarin 기반에 포함되어 있음*
- [x] Initialize-line-of-sight-cache-with-low-capacity.patch — *포팅 불필요: 이미 상위 최적화(Reduce line of sight updates)에 흡수되어 포함되어 있음*
- [ ] Leaves-Lithium-Sleeping-Block-Entity.patch — *보류: 2256줄 초대형 변경 (+fixup 495줄), 전용 세션에서 처리 권장*
- [x] Lithium-combined-heightmap-update.patch — *포팅 완료. 신규 유틸리티 클래스 net.caffeinemc.mods.lithium.common.world.chunk.heightmap.CombinedHeightmapUpdate 추가(4개 heightmap을 한 번의 top-down 스캔으로 동시 갱신), Heightmap.java에 isOpaque()/setHeight() public 접근자 추가*
- [x] Lithium-equipment-tracking.patch — *포팅 불가: 핵심 로직이 EntityEquipment.java(535줄 중 대부분)를 대상으로 하는데 1.21.4엔 그 클래스 자체가 없음 (Replace-entity-equipment-items-to-array와 동일 사유)*
- [ ] Lithium-faster-hash-palette.patch — *보류: 신규 LithiumHashPalette 전체 구현체(오픈 어드레싱 해시 기반 팔레트) 필요, 청크 블록 저장 압축 알고리즘이라 버그 시 월드 데이터 손상 리스크, 전용 세션에서 신중히 검증 권장*
- [ ] Luminol-Configurable-region-format-framework.patch — *보류: 월드 저장 파일 포맷 자체(리전 파일 I/O)를 교체 가능하게 만드는 초고위험 인프라 변경(Linear V2 등 대체 포맷 라이브러리 전체 필요), 월드 손상 리스크 매우 큼. 순수 최적화 백포트 범위를 넘어서는 별도 프로젝트급 작업으로 판단, 진행 안 함*
- [x] Make-EntityCollisionContext-a-live-representation.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [x] Move-random-tick-random.patch — *포팅 불필요: 이미 Gale/Pufferfish 기반에 포함되어 있음 (Level.java에 simpleRandom 필드 이미 존재)*
- [x] Only-update-frozen-ticks-if-changed.patch
- [x] Optimise-getEntities.patch
- [x] Optimize-PatchedDataComponentMap-equals.patch
- [x] Optimize-VarInt-write-and-VarLong-write.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음 (VarInt.java/VarLong.java에 이미 존재)*
- [x] Optimize-Vec3i-hashing.patch
- [x] Optimize-map-lookups-with-isEmpty-check.patch
- [x] Optimize-matching-item-checks.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (ItemStack.java isSameItem/isSameItemSameComponents에 stack == other 조기 return 이미 존재)*
- [x] Optimize-noise-generation.patch — *포팅 불필요: 이미 Gale/C2ME 기반에 포함되어 있음 (ImprovedNoise.java FLAT_SIMPLEX_GRAD 이미 존재)*
- [x] Optimize-pushable-selector.patch
- [x] Optimize-random-calls-in-chunk-ticking.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음 (LevelChunk.java에 shouldDoLightning 이미 존재)*
- [x] Optimize-respawn-anchor-explosion.patch — *포팅 완료. getFluidStateIfLoadedUnchecked 헬퍼가 1.21.4엔 없지만 동일 역할의 기존 Level#getFluidIfLoaded(BlockPos)로 대체 적용, stream 제거*
- [x] Optimize-sheep-offspring-color.patch — *포팅 불필요: 이미 Gale/carpet-fixes 기반에 포함되어 있음 (DyeColor.getMixedColor 이미 최적화됨)*
- [x] Optimize-sun-burn-tick.patch — *포팅 불필요: 이미 Gale/JettPack 기반에 포함되어 있음 (Entity.isSunBurnTick 이미 캐싱 적용됨)*
- [ ] Paper-PR-Optimise-temptation-lookups-changes.patch — *보류: 아래 항목과 함께 처리, 전용 세션 권장*
- [ ] Paper-PR-Optimise-temptation-lookups.patch — *보류: 33개 이상 파일(거의 모든 동물 몹 AI 클래스 + 신규 GlobalTemptationLookup 클래스)에 걸친 대규모 리라이트, 전용 세션 권장*
- [ ] Pluto-Expose-Direction-Plane-s-faces.patch — *보류: 692줄 대규모 변경, 전용 세션에서 처리 권장*
- [x] Pluto-don-t-load-chunks-to-spread-grass.patch — *포팅 완료. getChunkAtIfLoadedUnchecked가 1.21.4엔 없어 동일 역할의 기존 Level#getChunkIfLoaded(int,int)로 대체*
- [x] Pluto-reduce-allocation.patch — *포팅 완료 (WireHandler UpdateOrder.values() 캐싱, SpawnPlacementTypes 중복 BlockPos 로컬 제거)*
- [x] Pre-compute-VarLong-sizes.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음*
- [ ] Prevent-entities-from-moving-into-weak-loaded-chunks.patch — *보류: 8개 파일(ServerLevel + 여러 투사체 클래스) 변경 필요, 청크 상태 게이팅을 잘못 적용하면 투사체 동작 자체가 깨질 리스크가 있어 전용 세션에서 신중히 검증 권장*
- [x] Prevent-entities-random-strolling-into-non-ticking-c.patch — *포팅 불필요: 이미 Gale/MultiPaper 기반에 포함되어 있음*
- [x] Reduce-AbstractContainerMenu-allocations.patch
- [x] Reduce-RandomSource-instances.patch — *포팅 불필요: 이미 Gale/Patina 기반에 동일 최적화가 포함되어 있음 (Raid.java 등에 이미 존재)*
- [ ] Reduce-array-allocations.patch — *보류: 31개 파일에 걸친 대규모 변경 + 신규 유틸리티 클래스(me.titaniumtown.ArrayConstants) 필요, 전용 세션에서 처리 권장*
- [x] Reduce-block-destruction-packet-allocations.patch — *포팅 불필요: 이미 Gale/SportPaper 기반에 포함되어 있음*
- [x] Reduce-debug-subscribers-overhead.patch — *포팅 불필요: 1.21.4엔 debug subscribers 기능 자체가 없음 (ServerDebugSubscribers.java 클래스 부재, 더 최신 MC 버전 기능)*
- [x] Reduce-enderman-teleport-chunk-lookups.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음 (EnderMan.teleport 이미 single chunk lookup 적용됨)*
- [x] Reduce-in-wall-checks.patch — *포팅 불필요: 이미 Gale/Pufferfish 기반에 포함되어 있음 (LivingEntity.java에 checkStuckInWallInterval 로직 이미 존재)*
- [x] Reduce-lambda-and-Optional-allocation-in-EntityBased.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음*
- [x] Reduce-line-of-sight-updates-and-cache-lookups.patch — *포팅 불필요: 이미 Gale/Petal 기반에 포함되어 있음 (Sensing.java expiring 배열 구조 이미 존재)*
- [x] Reduce-optimiseRandomTick-new-BlockPos-instance-crea.patch — *포팅 완료. 4개 파일 .immutable() 안전 훅(RedstoneWireTurbo/SculkSpreader/TurtleEggBlock/ExperimentalRedstoneWireEvaluator) + ServerLevel#optimiseRandomTick의 POS_CACHE 공유 가변 필드 적용*
- [x] Reduce-projectile-chunk-loading.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [x] Reduce-skull-ItemStack-lookups-for-reduced-visibilit.patch — *포팅 불필요: 이미 Gale/Petal 기반에 포함되어 있음*
- [x] Reduce-villager-item-re-pickup.patch — *포팅 불필요: 이미 Gale/EMC 기반에 포함되어 있음*
- [x] Remove-iterators-from-Inventory.patch — *포팅 불가: 원본은 `this.equipment`(EnumMap 기반) + `EQUIPMENT_SLOT_MAPPING`/`EQUIPMENT_SLOTS_SORTED_BY_INDEX` 구조를 전제로 하는데 1.21.4 Inventory.java는 이 구조 자체가 없음(별도 armor/offhand NonNullList 구조), 상위 버전의 인벤토리 아키텍처 리팩터링에 의존적이라 포팅 불가*
- [x] Remove-lambda-from-ticking-guard.patch — *포팅 불필요: 이미 Gale/Airplane 기반에 포함되어 있음*
- [x] Remove-stream-in-CraftWorld-spawnParticle.patch — *포팅 완료. paper-patches 레이어 착수 후 ServerLevel#sendParticlesSourceBukkit 헬퍼 + CraftWorld#spawnParticle 호출부까지 모두 연결*
- [x] Remove-stream-in-MobSensor.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음 (변수명만 다름)*
- [x] Remove-stream-in-TemptingSensor.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Remove-stream-on-PlayerDetector.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Remove-stream-on-updateConnectedPlayersWithinRange.patch — *포팅 불필요: 이미 Leaf 기반에 포함되어 있음*
- [x] Replace-EntitySelectorOptions-map-with-optimized-col.patch
- [ ] Replace-brain-with-optimized-collection.patch — *보류: 신규 커스텀 컬렉션 3종(BehaviorControlArraySet/ActivityArrayMap/ActivityBitSet) 전체 구현 필요, Brain은 마을 사람/피글린 등 전체 몹 AI의 핵심 저장소라 버그 리스크 큼, 전용 세션 권장*
- [x] Replace-division-by-multiplication-in-CubePointRange.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음 (CubePointRange.java에 scale 필드 이미 존재)*
- [x] Replace-entity-equipment-items-to-array.patch — *포팅 불필요: 1.21.4엔 EntityEquipment 클래스 자체가 없음(장비를 별도 Map으로 관리하는 상위 버전의 리팩터링 이전 구조, 이미 Remove-iterators-from-Inventory 조사에서 동일하게 확인됨)*
- [x] Replace-parts-by-size-in-CubePointRange.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (CubePointRange.java에 size 필드 이미 존재)*
- [x] Replace-throttle-tracker-map-with-optimized-collecti.patch — *포팅 불필요: 이미 Gale/Dionysus 기반에 포함되어 있음 (ServerHandshakePacketListenerImpl.java에 이미 적용됨)*
- [ ] Rewrite-entity-despawn-time.patch — *보류: 엔티티 생명주기+청크시스템 광범위 변경, 전용 세션 권장*
- [ ] SIMD-support.patch — *보류: 실제 벡터화 로직을 담은 gg.pufferfish.pufferfish.simd.SIMDDetection 클래스 소스를 못 찾음(Leaf/Pufferfish 저장소 어디에도 plain 파일로 없음, 이 패치는 단지 `.initialize()` 호출부만 추가). 빌드엔 이미 `--add-modules=jdk.incubator.vector` 플래그만 선점되어 있고 실제 구현체는 없는 상태. 클래스 자체를 처음부터 작성해야 해서 전용 세션 권장*
- [x] Send-multiple-keep-alive-packets.patch — *포팅 불필요: 이미 Gale/Purpur 기반에 포함되어 있음*
- [x] Skip-BlockPhysicsEvent-if-no-listeners.patch — *포팅 완료(1.21.4는 원본과 달리 cworld != null 체크가 추가로 있어 두 조건을 함께 사용)*
- [x] Skip-PlayerCommandSendEvent-if-there-are-no-listener.patch — *포팅 불필요: 이미 Gale/Purpur 기반에 포함되어 있음 (Commands.java runSync에 이미 존재)*
- [x] Skip-PreCreatureSpawnEvent-if-no-listeners.patch — *포팅 완료(원본은 2개 메서드를 건드리지만 1.21.4엔 그 중 1개 메서드 형태만 존재해서 그 부분만 적용)*
- [x] Skip-VehicleEntityCollisionEvent-if-no-listeners.patch
- [x] Skip-cloning-advancement-criteria.patch — *포팅 불필요: 이미 Gale/Mirai 기반에 포함되어 있음 (Advancement 레코드 압축 생성자에 이미 적용됨)*
- [x] Skip-entity-move-if-movement-is-zero.patch — *포팅 불필요: 이미 Gale/VMP 기반에 포함되어 있음 (Entity.java에 boundingBoxChanged 필드 이미 존재)*
- [ ] Skip-inactive-entity-for-execute.patch — *보류: 신규 config 모듈 + Leaves ServerPhotographer 필요, 전용 세션 권장*
- [x] Skip-item-merge-checks-for-full-stacks.patch
- [x] Skip-negligible-planar-movement-multiplication.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (Entity.java에 oldDeltaMovement 가드 이미 존재)*
- [x] Skip-secondary-POI-sensor-if-absent.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음 (SecondaryPoiSensor.java에 이미 적용됨)*
- [x] Spread-out-sending-all-player-info.patch — *포팅 불필요: 이미 Gale/Purpur 기반에 포함되어 있음 (PlayerList.java에 sendAllPlayerInfoBuckets 이미 존재)*
- [x] Store-mob-counts-in-an-array.patch — *포팅 불필요: 이미 Gale/VMP 기반에 포함되어 있음 (LocalMobCapCalculator.java에 int[] counts 이미 존재)*
- [x] Update-boss-bar-within-tick.patch — *포팅 불필요: 이미 Gale/Lithium 기반에 포함되어 있음 (Raid.java에 isBarDirty 필드 이미 존재)*
- [x] Use-linked-map-for-entity-trackers.patch — *포팅 불필요: 이미 Gale/VMP 기반에 포함되어 있음 (ChunkMap.java entityMap이 이미 Int2ObjectLinkedOpenHashMap)*
- [x] Variable-entity-wake-up-duration.patch — *포팅 불필요: 이미 Gale 기반에 포함되어 있음 (ActivationRange.java에 entityWakeUpDurationRatioStandardDeviation 로직 이미 존재)*
- [x] Virtual-thread-support-for-chat-executor.patch — *포팅 완료 (VT4ChatExecutor config 모듈 + 0045-Virtual-thread-for-chat-executor.patch)*
- [x] Virtual-thread-support-for-download-pool.patch — *포팅 불필요/완료: 0145-More-virtual-threads 및 Paw-optimization에 통합되어 있음*
- [ ] async-chunk-sender.patch — *보류: 청크 패킷 직렬화를 백그라운드 스레드로 오프로드하는 기능. minecraft-patches 쪽(RegionizedPlayerChunkLoader.java)이 moonrise 청크 시스템의 핵심 전송 상태 머신을 건드리는 고위험 변경이라(신규 org.dreeam.leaf.async.chunk.AsyncChunkSender 유틸리티는 upstream에 존재 확인) 전용 세션에서 신중히 검증 권장. paper-patches 쪽(ChunkPacketBlockController 2개 파일)은 그 자체로는 의미 없고 이 항목에 종속*
- [x] cache-biome-for-mob-spawning-and-advancements.patch — *포팅 불필요: 이미 Leaf 자체 기반에 거의 동일한 형태로 포함되어 있음 (BiomeManager.getBiomeCached, OptimizeBiome config 모듈, NaturalSpawner/LocationPredicate 호출부 모두 이미 존재. 청크 패스트패스가 빠진 단일-인자 버전이지만 캐싱 자체는 동작함)*
- [x] cache-collision-list.patch
- [x] fast-bit-radix-sort.patch — *포팅 불필요: 이미 다른 형태(List<T>+Class 기반 API)로 구현되어 있음 (NearestItemSensor.itemSorter)*
- [ ] fixup-Leaves-Lithium-Sleeping-Block-Entity.patch — *보류: Leaves-Lithium-Sleeping-Block-Entity 종속, 그것과 함께 전용 세션에서 처리*
- [x] optimize-LevelChunk-getBlockStateFinal.patch
- [x] optimize-PalettedContainer-get.patch
- [x] optimize-PathNavigation-followThePath.patch — *포팅 완료 (Path#getNextNode() 직접 사용으로 getNextNodePos()의 Vec3i 할당 회피)*
- [x] optimize-SimpleBitStorage-object-layout.patch
- [x] optimize-applyMovementEmissionAndPlaySound.patch — *포팅 완료. getBlockStateIfLoadedUnchecked가 1.21.4엔 없어 동일 역할의 기존 Level#getBlockStateIfLoaded(BlockPos)로 대체*
- [ ] optimize-attribute.patch — *보류: AttributeInstanceArrayMap 등 대규모 신규 컬렉션 인프라 필요, 전용 세션 권장*
- [x] optimize-canHoldAnyFluid.patch
- [ ] optimize-checkInsideBlocks-calls.patch — *보류: upstream 대상 메서드가 `checkInsideBlocks(Vec3,Vec3,InsideBlockEffectApplier.StepBasedCollector,LongSet,int)`인데 1.21.4엔 `checkInsideBlocks(List<Entity.Movement>,Set<BlockState>)`로 완전히 다른(구버전) 아키텍처라 처음부터 재구현 필요, 전용 세션 권장*
- [x] optimize-collidedAlongVector.patch — *포팅 완료. 원본은 3개 호출부(Entity 2군데+Ghast)를 건드리지만 1.21.4는 entity-inside-block 충돌 코드가 구버전 구조라 호출부가 1개뿐이라 그 1곳에만 적용 (AABB#collidedAlongVector(Vec3,AABB) 단일-AABB 패스트패스 추가)*
- [ ] optimize-collision-shape.patch — *보류: 원본이 대부분의 블록에 대해 constantCollisionShape를 무조건 설정하는 방식으로 변경하는데, 1.21.4의 전체 Block 서브클래스 중 CollisionContext 의존적인 것이 upstream이 배제한 3종(Liquid/Scaffolding/PowderSnow) 외에 더 있는지 전수 검증이 필요해 리스크 높음, 전용 세션 권장*
- [x] optimize-get-chunk.patch — *Level#getBlockState(BlockPos) hunk만 포팅. SpreadingSnowyBlock.java 훅은 1.21.4에 해당 클래스가 없어(SpreadingSnowyDirtBlock으로 명칭 상이) 및 getChunkAtIfLoadedUnchecked 미존재로 스킵*
- [x] optimize-getOnPos.patch
- [ ] optimize-goal-selector.patch — *보류: 신규 커스텀 Set 구현체(org.dreeam.leaf.util.map.BinaryGoalSet) 전체를 새로 작성해야 함, GoalSelector 순회 순서 버그 시 전체 몹 AI가 깨질 리스크가 있어 전용 세션에서 신중히 검증 권장*
- [x] optimize-isStateClimbable.patch
- [ ] optimize-mob-despawn.patch — *보류: 신규 KDTree3D 유틸리티 + 신규 config 모듈(OptimizeDespawn) + Mob 디스폰 로직 전체 재구현(entity.checkDespawn()을 우회) 필요. 버그 시 테임된/네임태그 붙은 몹이 잘못 디스폰될 리스크가 있어 전용 세션에서 신중히 검증 권장. (paper-patches 레이어의 준비 훅인 optimize-despawn.patch — WorldConfiguration#despawnRanges EnumMap화 + DespawnRange 필드 public화 — 는 독자적으로 포팅 완료, DespawnMap 본체는 여전히 보류)*
- [x] optimize-movement-vector-normalization.patch — *포팅 불필요: 1.21.4의 Entity#checkFallDamage엔 이 최적화 대상인 8블록 clamp/normalize 로직 자체가 없음(더 최신 MC 버전에서 추가된 로직)*
- [x] optimize-no-action-time.patch — *포팅 완료. 신규 config 모듈 OptimizeNoActionTime 추가(disableLightCheck, 기본값 false)*
- [x] optimize-tickEffects.patch — *포팅 완료(1.21.4엔 ServerLevel 분기가 없는 더 단순한 구조라 그 구조에 맞춰 empty-check 가드만 적용)*
- [x] optimize-waypoint.patch — *포팅 불필요: 1.21.4엔 Waypoint(로케이터 바) 기능 자체가 없음(WaypointTransmitter 클래스 부재, 더 최신 MC 버전 기능)*
- [x] reduce-enchantment-allocations.patch
- [ ] remove-shouldTickBlocksAt-check.patch — *포팅 비권장: upstream 커밋 사유가 "BoundTickingBlockEntity#tick에 중복 체크 존재"인데 1.21.4엔 BoundTickingBlockEntity 클래스 자체가 없어 전제가 성립하지 않음*
- [x] rewrite-InsideBrownianWalk.patch — *포팅 불필요: 이미 Leaf 자체 최적화("Remove streams on InsideBrownianWalk")로 stream 제거 + 수동 루프 적용됨. 남은 차이(BlockAreaUtils 배열 + Fisher-Yates vs 현재의 ArrayList + Collections.shuffle)는 미미한 추가 이득이라 스킵*
- [ ] thread-unsafe-chunk-map.patch — *보류: moonrise 청크 시스템의 핵심 동시성 인프라(ChunkHolderManager)를 건드리는 고위험 패치. 신규 org.dreeam.leaf.world.ChunkCache 유틸리티 필요 + 잘못 포팅 시 청크 로딩 레이스 컨디션/월드 손상 리스크, 전용 세션에서 신중히 검증 권장*

## paper-patches (15개)

> `paper-server/.git` 워킹트리는 이미 존재했고(사전 설정됨), rebuild 태스크는 `leaf-server:rebuildPaperServerFeaturePatches`로 확인됨 (leaf-api의 `rebuildPaperApiFeaturePatches`에 대응). Batch 16에서 이 레이어를 처음 착수함.

- [x] Fish-Parallel-World-Ticking-API.patch — *포팅 완료. CraftServer#isParallelWorldTickingEnabled + CraftWorld#getTickTimes/getAverageTickTime, leaf-api의 Server.java/World.java에 대응 인터페이스 메서드 추가*
- [x] Leaf-Test-Async-Executor.patch — *범위 밖: 런타임 최적화가 아닌 JUnit 테스트 파일이고 @LeafTest 환경 애너테이션이 이 코드베이스에 없음, 최적화 백포트 범위에서 제외*
- [x] Optimize-VarInt-write-and-VarLong-write.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음 (VarInt.java/VarLong.java에 이미 존재)*
- [x] Optimize-block-entities-count.patch — *포팅 완료. CraftWorld#getTileEntityCount에 config-gated 단축 경로 추가(OptimizeBlockEntities.enabled, 기본값 true — 기존 코드베이스에 이미 존재하던 설정값)*
- [x] Pre-compute-VarLong-sizes.patch — *포팅 불필요: 이미 Gale 기반에 동일 최적화가 포함되어 있음*
- [ ] Reduce-array-allocations.patch — *보류: minecraft-patches의 동명 패치와 같은 me.titaniumtown.ArrayConstants 유틸리티에 종속, 그쪽과 함께 전용 세션에서 처리*
- [x] Remove-stream-in-CraftWorld-spawnParticle.patch
- [ ] SIMD-support.patch — *보류: bStats 메트릭 리포팅 훅뿐이라 사소하지만, 실제 SIMDDetection 클래스(minecraft-patches의 동명 패치와 공유)가 없어서 종속됨*
- [x] Use-optimized-collections-in-CB-classes.patch — *포팅 완료 (5개 파일: CraftBlockStates/CraftBossBar/CraftEntityTypes/CraftInventoryCreator/CraftMagicNumbers, HashMap→EnumMap/IdentityHashMap)*
- [x] Virtual-thread-support-for-bukkit-async-scheduler.patch — *포팅 완료 (VT4BukkitScheduler config 모듈 + paper 0016-Virtual-Thread-for-async-scheduler.patch)*
- [x] Virtual-thread-support-for-chat-executor.patch — *포팅 완료 (VT4ChatExecutor config 모듈 + 0045 패치)*
- [x] Virtual-thread-support-for-folia-async-scheduler.patch — *포팅 불필요: Folia 전용 기능으로 Paper/Bukkit 환경에는 해당 없음*
- [x] Virtual-thread-support.patch — *포팅 불필요/범위 밖: bStats 메트릭 리포팅 훅뿐이고 upstream 자체가 "Deprecated, remove in the future" 표시함, 실질적 기능 없음*
- [x] optimize-despawn.patch — *포팅 완료 (전체 2개 훅 모두 적용: WorldConfiguration#despawnRanges EnumMap화 + DespawnRange 필드 public화)*
- [x] optimize-mob-spawning.patch — *부분 포팅. CraftServer/CraftWorld의 spawnCategoryLimit Map→int[] 배열화는 완료. CustomChunkGenerator#getMobsAtChunk 훅은 InternalChunkGenerator 인터페이스에 해당 메서드 자체가 없어 스킵(더 큰 "청크 컨텍스트 전달" 리팩터링의 일부로 추정, 이번엔 미포함)*

## leaf-api (5개)

- [x] Cache-namespacedKey-toString-and-hash.patch
- [x] Fish-Parallel-World-Ticking-API.patch — *포팅 완료. paper-patches 레이어 착수 후 Server.java#isParallelWorldTickingEnabled + World.java#getTickTimes/getAverageTickTime 인터페이스 메서드와 CraftServer/CraftWorld 구현 모두 연결*
- [x] Player-canSee-by-entity-UUID.patch — *포팅 불필요: 이미 Gale/Purpur 기반에 포함되어 있음 (Player.java에 canSeePlayer(UUID) 선언 + CraftPlayer.java에 구현 모두 이미 존재)*
- [x] Replace-data-maps-with-optimized-collection.patch
- [ ] SIMD-support.patch — *보류: paper-patches/minecraft-patches의 동명 패치와 마찬가지로 실제 SIMDDetection 클래스가 없어서 종속됨*

**진행률: 112 / 138 체크됨** (실제 포팅 41개, 나머지는 이미 각종 서드파티 포크 기반에 구현되어 있거나 1.21.4엔 없는 기능이라 불필요로 확인됨.)

**Batch 18 (Config 버전 3.1 업데이트 + 보류 패치 포팅 완료)**: `LeafGlobalConfig`의 config-version을 `3.1`로 업데이트. `Reduce-optimiseRandomTick-new-BlockPos-instance-crea`의 남은 부분이었던 `ServerLevel.java` 내 `POS_CACHE` 공유 `MutableBlockPos` 최적화를 포팅 완료(`0232-reduce-optimiseRandomTick-new-BlockPos-instance-crea.patch`). Virtual-thread-support 4종은 이미 `VT4ChatExecutor`, `VT4BukkitScheduler`, `VT4ProfileExecutor`, `VT4UserAuthenticator` 개별 모듈 및 대응 패치(`0045`, `0046`, `0145`, paper `0016`)로 구현되어 있음을 재검증하고 체크 완료로 갱신.

**Batch 17**: `Fish-Parallel-World-Ticking-API`(leaf-api의 Server.java#isParallelWorldTickingEnabled + World.java#getTickTimes/getAverageTickTime 선언 + CraftServer/CraftWorld 구현 모두 연결, 기존에 이미 있던 SparklyPaperParallelWorldTicking 기능을 노출하는 모니터링 API), `optimize-mob-spawning`(CraftServer/CraftWorld의 spawnCategoryLimit Map→int[] 배열화 2개 훅 포팅, CustomChunkGenerator#getMobsAtChunk 훅은 InternalChunkGenerator에 해당 메서드가 없어 스킵)을 포팅. `Player-canSee-by-entity-UUID`는 이미 Gale/Purpur 기반에 선언+구현 모두 존재해 불필요 확인. `SIMD-support`는 실제 `gg.pufferfish.pufferfish.simd.SIMDDetection` 클래스를 Leaf/Pufferfish 어느 저장소에서도 못 찾음(빌드엔 `--add-modules=jdk.incubator.vector` 플래그만 선점되어 있고 실제 구현체 없음)이라 보류. Virtual-thread-support 4종 세트는 신규 config 모듈 및 executor 초기화 코드 자체가 전혀 없어 보류. Reduce-array-allocations(paper 레이어)는 minecraft-patches와 동일하게 ArrayConstants 유틸리티 부재로 보류. async-chunk-sender는 minecraft-patches 쪽 전체 패치(248줄, RegionizedPlayerChunkLoader.java의 청크 전송 상태 머신 핵심부 변경)까지 읽어봤고 실제 AsyncChunkSender 유틸리티는 upstream에 존재함을 확인했지만, 리스크가 커서 전용 세션으로 보류. 프레시 월드 3개 차원 부팅 스모크 테스트로 검증(자연 몹 스폰이 spawn limit 로직을 반복 실행하므로 관련 회귀 여부 특히 주의, 예외 0건).

**Batch 16 (paper-patches 레이어 최초 착수)**: `paper-server/.git` 워킹트리는 이미 존재했음을 확인, `leaf-server:rebuildPaperServerFeaturePatches` 태스크로 rebuild 가능함을 확인. `Optimize-block-entities-count`(CraftWorld#getTileEntityCount config-gated 단축 경로), `Remove-stream-in-CraftWorld-spawnParticle`(ServerLevel#sendParticlesSourceBukkit 헬퍼 신규 추가 + CraftWorld#spawnParticle 연결, minecraft-patches 레이어에도 함께 반영), `Use-optimized-collections-in-CB-classes`(5개 CraftBukkit 클래스의 HashMap→EnumMap/IdentityHashMap 교체)를 포팅. `optimize-despawn`의 준비 훅(WorldConfiguration#despawnRanges EnumMap화, DespawnRange 필드 public화)도 독자적으로 포팅했으나 DespawnMap 본체(별도 항목, optimize-mob-despawn)는 여전히 보류. `Leaf-Test-Async-Executor`는 런타임 최적화가 아닌 JUnit 테스트(+@LeafTest 애너테이션 부재)라 범위 밖으로 확인. 커밋 분리 중 사소한 git amend 실수가 있었으나(엉뚱한 커밋에 amend됨) `git diff base..HEAD --stat`으로 의도한 8개 파일이 정확히 반영됐는지 검증 후 진행. 프레시 월드 3개 차원 부팅 스모크 테스트(예외 0건) + 헤드리스 봇으로 엔티티 소환(/summon)과 파티클(/particle) 명령 실전 테스트까지 통과.

**Batch 15 (조사 위주, 신규 포팅 없음)**: Spread-out-sending-all-player-info는 이미 Gale/Purpur 기반에 구현되어 있어 불필요 확인. `Add-io_uring-support`는 실제로 시도해봄 — netty-incubator-transport-native-io_uring:0.0.26.Final 의존성(linux-x86_64/aarch_64 클래시파이어 확인됨)까지 추가했으나, 대상 클래스(EventLoopGroupHolder.java)가 1.21.4엔 존재하지 않고 훨씬 단순한 네트워크 부트스트랩 구조(ServerConnectionListener.java 안에서 NIO/Epoll만 직접 분기)라 핵심 접속 수락 로직을 직접 건드려야 해서 되돌림(빌드 의존성 변경도 원복 완료, git status 클린 확인). 나머지 대형 후보(Paper-PR-Optimise-temptation-lookups 2개, Luminol-Configurable-region-format-framework, Replace-brain-with-optimized-collection 등)는 각각 33개+ 파일/월드 저장 포맷/전체 몹 AI 저장소 급의 초대형·고위험 변경이라 스코프만 확인하고 보류 처리. leaf-api의 Fish-Parallel-World-Ticking-API/Player-canSee-by-entity-UUID/SIMD-support는 API 인터페이스만 있고 실제 구현이 미착수 paper-patches 레이어에 있어 보류. paper-patches(15개) 섹션 전체는 이번 세션에서 레이어 자체를 미착수.

**Batch 14**: `optimize-no-action-time`(신규 config 모듈 OptimizeNoActionTime 추가, disableLightCheck 기본값 false), `Lithium-combined-heightmap-update`(신규 유틸리티 클래스 `net.caffeinemc.mods.lithium.common.world.chunk.heightmap.CombinedHeightmapUpdate` 추가 — MOTION_BLOCKING/MOTION_BLOCKING_NO_LEAVES/OCEAN_FLOOR/WORLD_SURFACE 4개 heightmap을 한 번의 top-down 스캔으로 동시 갱신, Heightmap.java에 isOpaque()/setHeight() public 접근자 추가)를 포팅. cache-biome-for-mob-spawning-and-advancements는 이미 Leaf 자체 기반에 구현되어 있어 불필요, Replace-entity-equipment-items-to-array와 Lithium-equipment-tracking은 둘 다 1.21.4에 EntityEquipment 클래스가 없어 포팅 불가로 확인. optimize-checkInsideBlocks-calls(구버전 아키텍처), optimize-goal-selector(신규 커스텀 Set 전체 필요), thread-unsafe-chunk-map(청크 시스템 핵심 동시성 변경), Lithium-faster-hash-palette(신규 팔레트 알고리즘 전체 필요, 월드 데이터 손상 리스크), Leaves-Lithium-Sleeping-Block-Entity+fixup(2256+495줄 초대형)은 모두 고위험/대규모로 보류. 프레시 월드 3개 차원 부팅 스모크 테스트(예외 0건) + heightmap 전용 헤드리스 봇 검증(스폰 지점 아래 단단한 지형, 낙하 없음, 주변 9개 컬럼 지형 정상)까지 통과.

**Batch 13 (조사만, 신규 포팅 없음)**: cache-biome-for-mob-spawning-and-advancements는 이미 Leaf 자체 기반에 거의 동일하게 구현되어 있어 불필요로 확인, Replace-entity-equipment-items-to-array는 1.21.4엔 EntityEquipment 클래스 자체가 없어 포팅 불가로 확인. optimize-checkInsideBlocks-calls(대상 메서드 시그니처 자체가 다른 구버전 아키텍처), optimize-goal-selector(신규 커스텀 Set 구현체 전체 필요 + 몹 AI 전반 리스크), thread-unsafe-chunk-map(moonrise 청크 시스템 핵심 동시성 인프라 변경, 월드 손상 리스크)은 모두 고위험/대규모로 판단해 전용 세션으로 보류.

**Batch 12**: `optimize-applyMovementEmissionAndPlaySound`(getBlockStateIfLoadedUnchecked 미존재로 기존 Level#getBlockStateIfLoaded로 대체), `optimize-PathNavigation-followThePath`(Path#getNextNode() 직접 사용으로 getNextNodePos()의 Vec3i 할당 회피)를 포팅. 나머지 후보 중 5개는 이미 Gale/Airplane/Dionysus/VMP 기반에 구현되어 있었고(Better-checking-for-useless-move-packets, Optimize-random-calls-in-chunk-ticking, Use-linked-map-for-entity-trackers, Replace-throttle-tracker-map), rewrite-InsideBrownianWalk는 이미 Leaf 자체 stream 제거 최적화로 커버되어 있어 불필요, optimize-mob-despawn은 신규 KDTree3D 유틸+config 모듈+디스폰 로직 전체 재구현이 필요하고 버그 시 테임/네임태그 몹이 잘못 디스폰될 리스크가 있어 보류, Prevent-entities-from-moving-into-weak-loaded-chunks는 8개 파일(투사체 클래스 다수 포함) 규모라 보류. 프레시 월드 3개 차원 부팅 스모크 테스트로 검증, 예외 0건.

**Batch 11**: `optimize-tickEffects`(1.21.4의 더 단순한 구조에 맞춰 empty-check 가드 적용), `Pluto-reduce-allocation`(WireHandler UpdateOrder.values() 캐싱 + SpawnPlacementTypes 중복 BlockPos 제거), `Pluto-don-t-load-chunks-to-spread-grass`(getChunkAtIfLoadedUnchecked 미존재로 기존 Level#getChunkIfLoaded로 대체), `Filter-ClientboundSetEntityMotionPacket`(기존 ReduceUselessPackets config 모듈에 필드 추가, 기본값 false), `Optimize-respawn-anchor-explosion`(getFluidStateIfLoadedUnchecked 미존재로 기존 Level#getFluidIfLoaded로 대체), `optimize-collidedAlongVector`(1.21.4는 entity-inside-block 충돌 코드가 구버전 구조라 호출부 1곳에만 적용)를 포팅. 첫 컴파일 시도에서 2개 컴파일 에러 발견 후 수정: (1) `net.minecraft.world.entity.animal.squid.Squid` → 1.21.4엔 `net.minecraft.world.entity.animal.Squid`(서브패키지 없음), (2) `Direction.Plane.HORIZONTAL.faces`가 1.21.4에선 private 필드라 `Plane`이 구현하는 `Iterable<Direction>` 인터페이스로 순회하도록 수정. 나머지 후보 중 6개는 이미 Gale/MultiPaper 기반에 구현되어 있었고(Don-t-load-chunks-to-spawn-phantoms, Optimize-matching-item-checks), 2개는 해당 기능/코드 자체가 1.21.4에 없어 불필요(optimize-movement-vector-normalization: 8블록 clamp 로직 부재, optimize-waypoint: Waypoint 기능 자체 부재), Broadcast-crit-animations는 순수 최적화가 아닌 gameplay 수정이라 범위 밖으로 판단, optimize-collision-shape와 Pluto-Expose-Direction-Plane-s-faces는 리스크/규모 문제로 보류. 프레시 월드 3개 차원 부팅 스모크 테스트로 검증(컴파일 에러 수정 후 재테스트, 예외 0건).

**Batch 10**: `reduce-optimiseRandomTick-new-BlockPos-instance-crea`(4개 파일의 `.immutable()` 안전 훅만 포팅 — ServerLevel의 공유 POS_CACHE 최적화는 신규 config 모듈 필요로 스킵), `cache-world-generator-sea-level`(NoiseBasedChunkGenerator#getSeaLevel 캐싱)을 포팅. 나머지 후보 11개 중 9개는 이미 Gale 기반에 구현되어 있었고(Check-targeting-range, Reduce-in-wall-checks, Variable-entity-wake-up-duration, Update-boss-bar-within-tick, Skip-PlayerCommandSendEvent, Skip-negligible-planar-movement, Replace-division/parts-by-size-in-CubePointRange), Remove-iterators-from-Inventory는 1.21.4 인벤토리 구조 자체가 달라 포팅 불가로 확인, Reduce-array-allocations(31개 파일)와 Remove-stream-in-CraftWorld-spawnParticle(paper-patches 레이어 필요)은 대규모/미탐색 인프라 필요로 보류. 프레시 월드 3개 차원 부팅 스모크 테스트로 검증.

**Batch 9**: `optimize-SimpleBitStorage-object-layout`(불필요한 캐시된 long 필드 2개 제거, `cellIndex()`를 `Integer.toUnsignedLong()` 인라인 연산으로 재계산), `optimize-get-chunk`(`Level#getBlockState(BlockPos)`가 x/y/z를 로컬 변수로 뽑아 `chunk.getBlockState(x, y, z)` 오버로드 직접 호출, `BlockPos` 객체 재참조 감소 — 원본 패치의 SpreadingSnowyBlock.java 훅은 1.21.4에 해당 클래스/메서드 부재로 스킵)를 포팅. 프레시 월드로 3개 차원(overworld/nether/end) 전부 부팅 스모크 테스트, 예외 0건 확인.

**Phase 2 완료**: `Cache-block-state-tags` 기반 패치(BlockState에 `tagFlag` 캐시 필드 + `org.dreeam.leaf.util.BlockMasks` 유틸리티 추가; `pathType` 캐시는 1.21.4에 이미 별도로 존재해서 손댈 필요 없었음)를 실제로 포팅해서 `optimize-getOnPos`, `optimize-isStateClimbable`, `optimize-canHoldAnyFluid` 3개를 추가로 풀었음. 펜스/벽/펜스게이트/사다리/가루눈/트랩도어/덩굴/유체/가마솥 상호작용을 헤드리스 봇으로 전부 실전 테스트, 예외 0건.

기타 보류: Skip-inactive-entity-for-execute(신규 config 모듈 + Leaves ServerPhotographer 필요), Rewrite-entity-despawn-time(엔티티 생명주기+청크시스템 광범위 변경), optimize-attribute(AttributeInstanceArrayMap 등 대규모 신규 컬렉션 인프라 필요)**

## 포팅 절차 (참고)

1. `ver/26.2` 또는 `ver/1.21.11`에서 해당 패치 원문(`leaf-server/minecraft-patches/features/NNNN-*.patch`)을 확인
2. `leaf-server/src/minecraft/java` (paperweight 작업 트리, 별도 git repo)에서 대상 파일을 찾아 diff를 1.21.4 소스 기준으로 재적용
3. `git add` + `git commit` (커밋 메시지 = 패치 제목)
4. 루트에서 `JAVA_HOME=/usr/lib/jvm/java-21-openjdk-arm64 ./gradlew rebuildMinecraftFeaturePatches` 실행 → `leaf-server/minecraft-patches/features/`에 새 패치 파일 자동 생성
5. `./gradlew :leaf-server:compileJava` 로 컴파일 검증
6. 이 파일에 체크 표시 후 커밋