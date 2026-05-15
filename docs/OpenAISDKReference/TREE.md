# OpenAISDKReference Extracted Structure

Source: `docs/Docs&Examples.zip`

```text
OpenAISDKReference/
├── examples/
│   ├── agent_patterns/
│   │   ├── agents_as_tools.py
│   │   ├── agents_as_tools_conditional.py
│   │   ├── agents_as_tools_streaming.py
│   │   ├── agents_as_tools_structured.py
│   │   ├── deterministic.py
│   │   ├── forcing_tool_use.py
│   │   ├── human_in_the_loop.py
│   │   ├── human_in_the_loop_custom_rejection.py
│   │   ├── human_in_the_loop_stream.py
│   │   ├── input_guardrails.py
│   │   ├── llm_as_a_judge.py
│   │   ├── output_guardrails.py
│   │   ├── parallelization.py
│   │   ├── README.md
│   │   ├── routing.py
│   │   └── streaming_guardrails.py
│   ├── basic/
│   │   ├── media/
│   │   │   ├── image_bison.jpg
│   │   │   └── partial_o3-and-o4-mini-system-card.pdf
│   │   ├── agent_lifecycle_example.py
│   │   ├── dynamic_system_prompt.py
│   │   ├── hello_world.py
│   │   ├── hello_world_gpt_5.py
│   │   ├── hello_world_gpt_oss.py
│   │   ├── hello_world_jupyter.ipynb
│   │   ├── image_tool_output.py
│   │   ├── lifecycle_example.py
│   │   ├── local_file.py
│   │   ├── local_image.py
│   │   ├── non_strict_output_type.py
│   │   ├── previous_response_id.py
│   │   ├── prompt_template.py
│   │   ├── remote_image.py
│   │   ├── remote_pdf.py
│   │   ├── retry.py
│   │   ├── retry_litellm.py
│   │   ├── stream_function_call_args.py
│   │   ├── stream_items.py
│   │   ├── stream_text.py
│   │   ├── stream_ws.py
│   │   ├── tool_guardrails.py
│   │   ├── tools.py
│   │   └── usage_tracking.py
│   ├── customer_service/
│   │   └── main.py
│   ├── financial_research_agent/
│   │   ├── agents/
│   │   │   ├── __init__.py
│   │   │   ├── financials_agent.py
│   │   │   ├── planner_agent.py
│   │   │   ├── risk_agent.py
│   │   │   ├── search_agent.py
│   │   │   ├── verifier_agent.py
│   │   │   └── writer_agent.py
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── manager.py
│   │   ├── printer.py
│   │   └── README.md
│   ├── handoffs/
│   │   ├── message_filter.py
│   │   └── message_filter_streaming.py
│   ├── hosted_mcp/
│   │   ├── __init__.py
│   │   ├── connectors.py
│   │   ├── human_in_the_loop.py
│   │   ├── on_approval.py
│   │   └── simple.py
│   ├── mcp/
│   │   ├── filesystem_example/
│   │   │   ├── sample_files/
│   │   │   │   ├── favorite_books.txt
│   │   │   │   ├── favorite_cities.txt
│   │   │   │   └── favorite_songs.txt
│   │   │   ├── main.py
│   │   │   └── README.md
│   │   ├── get_all_mcp_tools_example/
│   │   │   ├── sample_files/
│   │   │   │   ├── books.txt
│   │   │   │   └── favorite_songs.txt
│   │   │   ├── main.py
│   │   │   └── README.md
│   │   ├── git_example/
│   │   │   ├── main.py
│   │   │   └── README.md
│   │   ├── manager_example/
│   │   │   ├── app.py
│   │   │   ├── mcp_server.py
│   │   │   ├── README.md
│   │   │   └── smoke_test.py
│   │   ├── prompt_server/
│   │   │   ├── main.py
│   │   │   ├── README.md
│   │   │   └── server.py
│   │   ├── sse_example/
│   │   │   ├── main.py
│   │   │   ├── README.md
│   │   │   └── server.py
│   │   ├── sse_remote_example/
│   │   │   ├── main.py
│   │   │   └── README.md
│   │   ├── streamable_http_remote_example/
│   │   │   ├── main.py
│   │   │   └── README.md
│   │   ├── streamablehttp_custom_client_example/
│   │   │   ├── main.py
│   │   │   ├── README.md
│   │   │   └── server.py
│   │   ├── streamablehttp_example/
│   │   │   ├── main.py
│   │   │   ├── README.md
│   │   │   └── server.py
│   │   └── tool_filter_example/
│   │       ├── sample_files/
│   │       │   ├── books.txt
│   │       │   └── favorite_songs.txt
│   │       ├── main.py
│   │       └── README.md
│   ├── memory/
│   │   ├── advanced_sqlite_session_example.py
│   │   ├── compaction_session_example.py
│   │   ├── compaction_session_stateless_example.py
│   │   ├── dapr_session_example.py
│   │   ├── encrypted_session_example.py
│   │   ├── file_hitl_example.py
│   │   ├── file_session.py
│   │   ├── hitl_session_scenario.py
│   │   ├── memory_session_hitl_example.py
│   │   ├── openai_session_example.py
│   │   ├── openai_session_hitl_example.py
│   │   ├── redis_session_example.py
│   │   ├── sqlalchemy_session_example.py
│   │   └── sqlite_session_example.py
│   ├── model_providers/
│   │   ├── any_llm_auto.py
│   │   ├── any_llm_provider.py
│   │   ├── custom_example_agent.py
│   │   ├── custom_example_global.py
│   │   ├── custom_example_provider.py
│   │   ├── litellm_auto.py
│   │   ├── litellm_provider.py
│   │   └── README.md
│   ├── realtime/
│   │   ├── app/
│   │   │   ├── static/
│   │   │   │   ├── app.js
│   │   │   │   ├── audio-playback.worklet.js
│   │   │   │   ├── audio-recorder.worklet.js
│   │   │   │   ├── favicon.ico
│   │   │   │   └── index.html
│   │   │   ├── agent.py
│   │   │   ├── README.md
│   │   │   └── server.py
│   │   ├── cli/
│   │   │   └── demo.py
│   │   ├── twilio/
│   │   │   ├── __init__.py
│   │   │   ├── README.md
│   │   │   ├── requirements.txt
│   │   │   ├── server.py
│   │   │   └── twilio_handler.py
│   │   └── twilio_sip/
│   │       ├── __init__.py
│   │       ├── agents.py
│   │       ├── README.md
│   │       ├── requirements.txt
│   │       └── server.py
│   ├── reasoning_content/
│   │   ├── __init__.py
│   │   ├── gpt_oss_stream.py
│   │   ├── main.py
│   │   └── runner_example.py
│   ├── research_bot/
│   │   ├── agents/
│   │   │   ├── __init__.py
│   │   │   ├── planner_agent.py
│   │   │   ├── search_agent.py
│   │   │   └── writer_agent.py
│   │   ├── sample_outputs/
│   │   │   ├── product_recs.md
│   │   │   ├── product_recs.txt
│   │   │   ├── vacation.md
│   │   │   └── vacation.txt
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── manager.py
│   │   ├── printer.py
│   │   └── README.md
│   ├── sandbox/
│   │   ├── data/
│   │   │   ├── f1040.pdf
│   │   │   └── sample_w2.pdf
│   │   ├── docker/
│   │   │   ├── mounts/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── azure_mount_read_write.py
│   │   │   │   ├── gcs_mount_read_write.py
│   │   │   │   ├── mount_smoke.py
│   │   │   │   ├── s3_files_mount_read_write.py
│   │   │   │   └── s3_mount_read_write.py
│   │   │   ├── __init__.py
│   │   │   ├── docker_runner.py
│   │   │   └── Dockerfile.mount
│   │   ├── docs/
│   │   │   ├── repo/
│   │   │   │   ├── tests/
│   │   │   │   │   └── test_credit_note.sh
│   │   │   │   ├── credit_note.sh
│   │   │   │   ├── README.md
│   │   │   │   └── task.md
│   │   │   ├── skills/
│   │   │   │   └── credit-note-fixer/
│   │   │   │       └── SKILL.md
│   │   │   ├── __init__.py
│   │   │   └── coding_task.py
│   │   ├── extensions/
│   │   │   ├── daytona/
│   │   │   │   ├── usaspending_text2sql/
│   │   │   │   │   ├── schema/
│   │   │   │   │   │   ├── tables/
│   │   │   │   │   │   │   └── spending.md
│   │   │   │   │   │   ├── glossary.md
│   │   │   │   │   │   └── overview.md
│   │   │   │   │   ├── __init__.py
│   │   │   │   │   ├── agent.py
│   │   │   │   │   ├── README.md
│   │   │   │   │   ├── setup_db.py
│   │   │   │   │   └── sql_capability.py
│   │   │   │   ├── __init__.py
│   │   │   │   └── daytona_runner.py
│   │   │   ├── runloop/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── capabilities.py
│   │   │   │   └── runner.py
│   │   │   ├── temporal/
│   │   │   │   ├── _worker_setup.py
│   │   │   │   ├── justfile
│   │   │   │   ├── local_hello_workflow.py
│   │   │   │   ├── README.md
│   │   │   │   ├── temporal_sandbox_agent.py
│   │   │   │   ├── temporal_sandbox_tui.py
│   │   │   │   └── temporal_session_manager.py
│   │   │   ├── __init__.py
│   │   │   ├── blaxel_runner.py
│   │   │   ├── cloudflare_runner.py
│   │   │   ├── e2b_runner.py
│   │   │   ├── modal_runner.py
│   │   │   ├── README.md
│   │   │   └── vercel_runner.py
│   │   ├── healthcare_support/
│   │   │   ├── data/
│   │   │   │   ├── fixtures/
│   │   │   │   │   ├── insurance_eligibility.json
│   │   │   │   │   ├── patient_profiles.json
│   │   │   │   │   └── referral_status.json
│   │   │   │   └── scenarios/
│   │   │   │       ├── billing_coverage_clarification.json
│   │   │   │       ├── blue_cross_pt_benefits.json
│   │   │   │       ├── eligibility_verification_basic.json
│   │   │   │       ├── messy_ambiguous_knee_case.json
│   │   │   │       ├── prior_auth_confusion_ct.json
│   │   │   │       └── referral_status_check.json
│   │   │   ├── policies/
│   │   │   │   ├── auth_review_queue_routing.md
│   │   │   │   ├── billing_after_consult_faq.md
│   │   │   │   ├── blue_cross_benefits_reference.md
│   │   │   │   ├── blue_cross_ppo_prior_auth.md
│   │   │   │   ├── blue_cross_referral_rules.md
│   │   │   │   ├── commercial_eligibility_checklist.md
│   │   │   │   ├── human_escalation_policy.md
│   │   │   │   ├── knee_surgery_medical_necessity.md
│   │   │   │   ├── orthopedic_imaging_policy.md
│   │   │   │   ├── outbound_fax_packet_requirements.md
│   │   │   │   ├── patient_messaging_guidelines.md
│   │   │   │   ├── referral_pending_sop.md
│   │   │   │   └── scheduling_hold_policy.md
│   │   │   ├── skills/
│   │   │   │   └── prior-auth-packet-builder/
│   │   │   │       └── SKILL.md
│   │   │   ├── __init__.py
│   │   │   ├── data.py
│   │   │   ├── main.py
│   │   │   ├── models.py
│   │   │   ├── README.md
│   │   │   ├── support_agents.py
│   │   │   ├── tools.py
│   │   │   └── workflow.py
│   │   ├── misc/
│   │   │   ├── __init__.py
│   │   │   ├── example_support.py
│   │   │   ├── reference_policy_mcp_server.py
│   │   │   ├── workspace_apply_patch.py
│   │   │   └── workspace_shell.py
│   │   ├── tutorials/
│   │   │   ├── data/
│   │   │   │   └── dataroom/
│   │   │   │       └── setup.py
│   │   │   ├── dataroom_metric_extract/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── evals.py
│   │   │   │   ├── main.py
│   │   │   │   ├── README.md
│   │   │   │   └── schemas.py
│   │   │   ├── dataroom_qa/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── main.py
│   │   │   │   └── README.md
│   │   │   ├── repo_code_review/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── evals.py
│   │   │   │   ├── main.py
│   │   │   │   └── README.md
│   │   │   ├── sandbox_resume/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── main.py
│   │   │   │   └── README.md
│   │   │   ├── vision_website_clone/
│   │   │   │   ├── skills/
│   │   │   │   │   └── playwright/
│   │   │   │   │       └── SKILL.md
│   │   │   │   ├── __init__.py
│   │   │   │   ├── main.py
│   │   │   │   ├── README.md
│   │   │   │   └── reference-site.png
│   │   │   ├── __init__.py
│   │   │   ├── Dockerfile
│   │   │   └── misc.py
│   │   ├── __init__.py
│   │   ├── basic.py
│   │   ├── handoffs.py
│   │   ├── memory.py
│   │   ├── memory_multi_agent_multiturn.py
│   │   ├── memory_s3.py
│   │   ├── README.md
│   │   ├── sandbox_agent_capabilities.py
│   │   ├── sandbox_agent_with_remote_snapshot.py
│   │   ├── sandbox_agent_with_tools.py
│   │   ├── sandbox_agents_as_tools.py
│   │   ├── tax_prep.py
│   │   ├── unix_local_pty.py
│   │   └── unix_local_runner.py
│   ├── tools/
│   │   ├── skills/
│   │   │   └── csv-workbench/
│   │   │       ├── playbook.md
│   │   │       └── SKILL.md
│   │   ├── apply_patch.py
│   │   ├── code_interpreter.py
│   │   ├── codex.py
│   │   ├── codex_same_thread.py
│   │   ├── computer_use.py
│   │   ├── container_shell_inline_skill.py
│   │   ├── container_shell_skill_reference.py
│   │   ├── file_search.py
│   │   ├── image_generator.py
│   │   ├── local_shell_skill.py
│   │   ├── shell.py
│   │   ├── shell_human_in_the_loop.py
│   │   ├── tool_search.py
│   │   ├── web_search.py
│   │   └── web_search_filters.py
│   ├── voice/
│   │   ├── static/
│   │   │   ├── __init__.py
│   │   │   ├── main.py
│   │   │   ├── README.md
│   │   │   └── util.py
│   │   ├── streamed/
│   │   │   ├── __init__.py
│   │   │   ├── main.py
│   │   │   ├── my_workflow.py
│   │   │   └── README.md
│   │   └── __init__.py
│   ├── __init__.py
│   ├── auto_mode.py
│   └── run_examples.py
├── models/
│   ├── index.md
│   └── litellm.md
├── realtime/
│   ├── guide.md
│   ├── quickstart.md
│   └── transport.md
├── ref/
│   ├── extensions/
│   │   ├── experimental/
│   │   │   └── codex/
│   │   │       ├── codex.md
│   │   │       ├── codex_options.md
│   │   │       ├── codex_tool.md
│   │   │       ├── events.md
│   │   │       ├── exec.md
│   │   │       ├── items.md
│   │   │       ├── output_schema_file.md
│   │   │       ├── payloads.md
│   │   │       ├── thread.md
│   │   │       ├── thread_options.md
│   │   │       └── turn_options.md
│   │   ├── memory/
│   │   │   ├── advanced_sqlite_session.md
│   │   │   ├── async_sqlite_session.md
│   │   │   ├── dapr_session.md
│   │   │   ├── encrypt_session.md
│   │   │   ├── mongodb_session.md
│   │   │   ├── redis_session.md
│   │   │   └── sqlalchemy_session.md
│   │   ├── models/
│   │   │   ├── any_llm_model.md
│   │   │   ├── any_llm_provider.md
│   │   │   ├── litellm_model.md
│   │   │   └── litellm_provider.md
│   │   ├── sandbox/
│   │   │   ├── blaxel/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   ├── cloudflare/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   ├── daytona/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   ├── e2b/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   ├── modal/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   ├── runloop/
│   │   │   │   ├── mounts.md
│   │   │   │   └── sandbox.md
│   │   │   └── vercel/
│   │   │       └── sandbox.md
│   │   ├── handoff_filters.md
│   │   ├── handoff_prompt.md
│   │   ├── litellm.md
│   │   ├── tool_output_trimmer.md
│   │   └── visualization.md
│   ├── handoffs/
│   │   └── history.md
│   ├── mcp/
│   │   ├── manager.md
│   │   ├── server.md
│   │   └── util.md
│   ├── memory/
│   │   ├── openai_conversations_session.md
│   │   ├── openai_responses_compaction_session.md
│   │   ├── session.md
│   │   ├── session_settings.md
│   │   ├── sqlite_session.md
│   │   └── util.md
│   ├── models/
│   │   ├── chatcmpl_converter.md
│   │   ├── chatcmpl_helpers.md
│   │   ├── chatcmpl_stream_handler.md
│   │   ├── default_models.md
│   │   ├── fake_id.md
│   │   ├── interface.md
│   │   ├── multi_provider.md
│   │   ├── openai_agent_registration.md
│   │   ├── openai_chatcompletions.md
│   │   ├── openai_client_utils.md
│   │   ├── openai_provider.md
│   │   ├── openai_responses.md
│   │   └── reasoning_content_replay.md
│   ├── realtime/
│   │   ├── agent.md
│   │   ├── audio_formats.md
│   │   ├── config.md
│   │   ├── events.md
│   │   ├── handoffs.md
│   │   ├── items.md
│   │   ├── model.md
│   │   ├── model_events.md
│   │   ├── model_inputs.md
│   │   ├── openai_realtime.md
│   │   ├── runner.md
│   │   └── session.md
│   ├── run_internal/
│   │   ├── agent_bindings.md
│   │   ├── agent_runner_helpers.md
│   │   ├── approvals.md
│   │   ├── error_handlers.md
│   │   ├── guardrails.md
│   │   ├── items.md
│   │   ├── model_retry.md
│   │   ├── oai_conversation.md
│   │   ├── prompt_cache_key.md
│   │   ├── run_grouping.md
│   │   ├── run_loop.md
│   │   ├── run_steps.md
│   │   ├── session_persistence.md
│   │   ├── streaming.md
│   │   ├── tool_actions.md
│   │   ├── tool_execution.md
│   │   ├── tool_planning.md
│   │   ├── tool_use_tracker.md
│   │   ├── turn_preparation.md
│   │   └── turn_resolution.md
│   ├── sandbox/
│   │   ├── capabilities/
│   │   │   ├── tools/
│   │   │   │   ├── apply_patch_tool.md
│   │   │   │   ├── shell_tool.md
│   │   │   │   └── view_image.md
│   │   │   ├── capabilities.md
│   │   │   ├── capability.md
│   │   │   ├── compaction.md
│   │   │   ├── filesystem.md
│   │   │   ├── memory.md
│   │   │   ├── shell.md
│   │   │   └── skills.md
│   │   ├── entries/
│   │   │   ├── mounts/
│   │   │   │   ├── providers/
│   │   │   │   │   ├── azure_blob.md
│   │   │   │   │   ├── base.md
│   │   │   │   │   ├── box.md
│   │   │   │   │   ├── gcs.md
│   │   │   │   │   ├── r2.md
│   │   │   │   │   ├── s3.md
│   │   │   │   │   └── s3_files.md
│   │   │   │   ├── base.md
│   │   │   │   └── patterns.md
│   │   │   ├── artifacts.md
│   │   │   └── base.md
│   │   ├── memory/
│   │   │   ├── interface.md
│   │   │   ├── manager.md
│   │   │   ├── phase_one.md
│   │   │   ├── phase_two.md
│   │   │   ├── prompts.md
│   │   │   ├── rollouts.md
│   │   │   └── storage.md
│   │   ├── sandboxes/
│   │   │   ├── docker.md
│   │   │   └── unix_local.md
│   │   ├── session/
│   │   │   ├── archive_extraction.md
│   │   │   ├── archive_ops.md
│   │   │   ├── base_sandbox_session.md
│   │   │   ├── dependencies.md
│   │   │   ├── events.md
│   │   │   ├── manager.md
│   │   │   ├── manifest_application.md
│   │   │   ├── manifest_ops.md
│   │   │   ├── mount_lifecycle.md
│   │   │   ├── pty_types.md
│   │   │   ├── runtime_helpers.md
│   │   │   ├── sandbox_client.md
│   │   │   ├── sandbox_session.md
│   │   │   ├── sandbox_session_state.md
│   │   │   ├── sinks.md
│   │   │   ├── snapshot_lifecycle.md
│   │   │   ├── tar_workspace.md
│   │   │   ├── utils.md
│   │   │   └── workspace_payloads.md
│   │   ├── util/
│   │   │   ├── checksums.md
│   │   │   ├── deep_merge.md
│   │   │   ├── github.md
│   │   │   ├── iterator_io.md
│   │   │   ├── parse_utils.md
│   │   │   ├── retry.md
│   │   │   ├── tar_utils.md
│   │   │   └── token_truncation.md
│   │   ├── apply_patch.md
│   │   ├── config.md
│   │   ├── entries.md
│   │   ├── errors.md
│   │   ├── files.md
│   │   ├── manifest.md
│   │   ├── manifest_render.md
│   │   ├── materialization.md
│   │   ├── permissions.md
│   │   ├── remote_mount_policy.md
│   │   ├── runtime.md
│   │   ├── runtime_agent_preparation.md
│   │   ├── runtime_session_manager.md
│   │   ├── sandbox_agent.md
│   │   ├── snapshot.md
│   │   ├── snapshot_defaults.md
│   │   ├── types.md
│   │   └── workspace_paths.md
│   ├── tracing/
│   │   ├── config.md
│   │   ├── context.md
│   │   ├── create.md
│   │   ├── index.md
│   │   ├── logger.md
│   │   ├── model_tracing.md
│   │   ├── processor_interface.md
│   │   ├── processors.md
│   │   ├── provider.md
│   │   ├── scope.md
│   │   ├── setup.md
│   │   ├── span_data.md
│   │   ├── spans.md
│   │   ├── traces.md
│   │   └── util.md
│   ├── voice/
│   │   ├── models/
│   │   │   ├── openai_model_provider.md
│   │   │   ├── openai_provider.md
│   │   │   ├── openai_stt.md
│   │   │   └── openai_tts.md
│   │   ├── events.md
│   │   ├── exceptions.md
│   │   ├── imports.md
│   │   ├── input.md
│   │   ├── model.md
│   │   ├── pipeline.md
│   │   ├── pipeline_config.md
│   │   ├── result.md
│   │   ├── utils.md
│   │   └── workflow.md
│   ├── agent.md
│   ├── agent_output.md
│   ├── agent_tool_input.md
│   ├── agent_tool_state.md
│   ├── apply_diff.md
│   ├── computer.md
│   ├── editor.md
│   ├── exceptions.md
│   ├── function_schema.md
│   ├── guardrail.md
│   ├── handoffs.md
│   ├── index.md
│   ├── items.md
│   ├── lifecycle.md
│   ├── logger.md
│   ├── memory.md
│   ├── model_settings.md
│   ├── prompts.md
│   ├── repl.md
│   ├── responses_websocket_session.md
│   ├── result.md
│   ├── retry.md
│   ├── run.md
│   ├── run_config.md
│   ├── run_context.md
│   ├── run_error_handlers.md
│   ├── run_state.md
│   ├── sandbox.md
│   ├── stream_events.md
│   ├── strict_schema.md
│   ├── tool.md
│   ├── tool_context.md
│   ├── tool_guardrails.md
│   ├── usage.md
│   └── version.md
├── sandbox/
│   ├── clients.md
│   ├── guide.md
│   └── memory.md
├── scripts/
│   ├── generate_ref_files.py
│   └── translate_docs.py
├── sessions/
│   ├── advanced_sqlite_session.md
│   ├── encrypted_session.md
│   ├── index.md
│   └── sqlalchemy_session.md
├── stylesheets/
│   └── extra.css
├── voice/
│   ├── pipeline.md
│   ├── quickstart.md
│   └── tracing.md
├── zh/
│   ├── models/
│   │   ├── index.md
│   │   └── litellm.md
│   ├── realtime/
│   │   ├── guide.md
│   │   ├── quickstart.md
│   │   └── transport.md
│   ├── sandbox/
│   │   ├── clients.md
│   │   ├── guide.md
│   │   └── memory.md
│   ├── sessions/
│   │   ├── advanced_sqlite_session.md
│   │   ├── encrypted_session.md
│   │   ├── index.md
│   │   └── sqlalchemy_session.md
│   ├── voice/
│   │   ├── pipeline.md
│   │   ├── quickstart.md
│   │   └── tracing.md
│   ├── agents.md
│   ├── config.md
│   ├── context.md
│   ├── examples.md
│   ├── guardrails.md
│   ├── handoffs.md
│   ├── human_in_the_loop.md
│   ├── index.md
│   ├── mcp.md
│   ├── multi_agent.md
│   ├── quickstart.md
│   ├── release.md
│   ├── repl.md
│   ├── results.md
│   ├── running_agents.md
│   ├── sandbox_agents.md
│   ├── sessions.md
│   ├── streaming.md
│   ├── tools.md
│   ├── tracing.md
│   ├── usage.md
│   └── visualization.md
├── agents.md
├── config.md
├── context.md
├── examples.md
├── guardrails.md
├── handoffs.md
├── human_in_the_loop.md
├── index.md
├── llms-full.txt
├── llms.txt
├── mcp.md
├── multi_agent.md
├── quickstart.md
├── release.md
├── repl.md
├── results.md
├── running_agents.md
├── sandbox_agents.md
├── streaming.md
├── tools.md
├── tracing.md
├── usage.md
└── visualization.md
```
