SET(LIB_NAME osgVerseAnimation)
SET(LIBRARY_INCLUDE_FILES
    PlayerAnimation.h TweenAnimation.h BlendShapeAnimation.h
    PhysicsEngine.h Utilities.h)
SET(LIBRARY_FILES ${LIBRARY_INCLUDE_FILES}
    PlayerAnimation.cpp PlayerAnimationInternal.h PlayerAnimationInternal.cpp
    TweenAnimation.cpp BlendShapeAnimation.cpp)

IF(BULLET_FOUND)
	SET(LIBRARY_FILES ${LIBRARY_FILES} PhysicsEngine.cpp Utilities.cpp)
ENDIF(BULLET_FOUND)

NEW_LIBRARY(${LIB_NAME} STATIC)
TARGET_LINK_LIBRARIES(${LIB_NAME} osgVerseDependency osgVerseModeling)
TARGET_COMPILE_OPTIONS(${LIB_NAME} PUBLIC -D_SCL_SECURE_NO_WARNINGS)
IF(BULLET_FOUND)
    TARGET_LINK_LIBRARIES(${LIB_NAME} debug BulletDynamics${VERSE_DEBUG_POSTFIX} optimized BulletDynamics)
    TARGET_LINK_LIBRARIES(${LIB_NAME} debug BulletCollision${VERSE_DEBUG_POSTFIX} optimized BulletCollision)
    TARGET_LINK_LIBRARIES(${LIB_NAME} debug LinearMath${VERSE_DEBUG_POSTFIX} optimized LinearMath)
ENDIF(BULLET_FOUND)

INSTALL(TARGETS ${LIB_NAME} EXPORT ${LIB_NAME}
        RUNTIME DESTINATION ${INSTALL_BINDIR} COMPONENT libosgverse
        LIBRARY DESTINATION ${INSTALL_LIBDIR} COMPONENT libosgverse
        ARCHIVE DESTINATION ${INSTALL_ARCHIVEDIR} COMPONENT libosgverse-dev)
INSTALL(FILES ${LIBRARY_INCLUDE_FILES} DESTINATION ${INSTALL_INCDIR}/osgVerse/animation COMPONENT libosgverse-dev)
